# Using local filesystem Envoy xDS

```mermaid
graph TD;
    subgraph echo_cluster
    echo1;
    echo2;
    echo3;
    echo4;
    end

    client -->|http/80| envoy;
    envoy -->|http/8080| echo1;
    envoy -->|http/8080| echo2;
    envoy -->|http/8080| echo3;
    envoy -->|http/8080| echo4;
```

1. Start Docker containers
    ```command
    docker compose up -d
    ```
1. Verify `echo` cluster is added via xDS API
    ```command
    % curl -sSLD/dev/stderr http://localhost:9901/clusters | grep added_via_api
    HTTP/1.1 200 OK
    content-type: text/plain; charset=UTF-8
    cache-control: no-cache, max-age=0
    x-content-type-options: nosniff
    date: Tue, 21 Nov 2023 09:51:31 GMT
    server: envoy
    transfer-encoding: chunked

    echo::added_via_api::true
    ```
1. Cleanup Docker containers
    ```command
    docker compose down --remove-orphans --volumes
    ```
