# Using gRPC Envoy xDS

```command
% curl -sSLD/dev/stderr 0:9901/clusters | grep added_via_api
HTTP/1.1 200 OK
content-type: text/plain; charset=UTF-8
cache-control: no-cache, max-age=0
x-content-type-options: nosniff
date: Tue, 21 Nov 2023 09:51:31 GMT
server: envoy
transfer-encoding: chunked

echo::added_via_api::true
```
