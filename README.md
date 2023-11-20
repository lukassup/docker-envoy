# docker-envoy

Envoy demo with Docker

1. Start containers in compose file
    ```sh
    docker compose up -d
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
1. Run chaos monkey
    ```sh
    while n=$(shuf -i1-4 -n1); do docker compose stop echo${n}; sleep 1; docker compose start echo${n}; sleep 1; done
    ```
