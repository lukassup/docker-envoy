# docker-envoy

Envoy demo with Docker


1. Start containers in compose file
    ```sh
    docker compose up -d
    ```
    or with Consul SD
    ```sh
    docker compose -f docker-compose.consul.yml up -d
    ```
1. Make requests to proxy
    ```sh
    watch -d -n1 -- curl -sSLD/dev/stderr http://localhost
    ```
1. Tail envoy logs
    ```sh
    docker compose logs envoy -f
    ```
1. Inspect Envoy stats
    ```sh
    curl -sSLD/dev/stderr http://localhost:9901/stats
    ```
1. Verify load balancing algorithms
    ```sh
    for (( c=1; c<=1000; c++ )); do curl -sS http://localhost; done | sort | uniq -c
    ```
1. Run chaos monkey
    ```sh
    while n=$(shuf -i1-4 -n1); do docker compose stop echo${n}; sleep 1; docker compose start echo${n}; sleep 1; done
    ```
1. Run load test
   ```sh
   wrk -t12 -c400 -d60s http://localhost/
   ```
