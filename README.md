# metrics
This project implements a golang simple Reverse Proxy that exports HTTP metrics to Prometheus.

Inspired by
- [Reverse Proxy with Prometheus Export](https://github.com/FerdinandvHagen/reverse-proxy)
- [Smart Rate Limiter in Go](https://medium.com/lightbaseio/smart-rate-limiter-in-go-9850b6fb12dd)

## Exported Metrics
The proxy will export the following metrics:

- default metrics from the Go runtime
- `http_requests_total (method, path, status)` - a counter for the number of HTTP requests
    - `method` is the HTTP method (GET, POST, etc.)
    - `path` is the URL path
    - `status` is the HTTP status code (i.e. 2xx, 3xx, 4xx, 5xx)
- `http_response_time_seconds (method, path)` - a histogram of the request duration
    - `method` is the HTTP method (GET, POST, etc.)
    - `path` is the URL path
- `http_errors_total` - a counter for status code of the reverse proxy
- `http_remote_addrs_total` - a counter for `X-Forwarded-For` header

## Features
- http only, no TLS
- routing path matching before counting metrics
- exports HTTP metrics to Prometheus
- whitelist and blacklist
- flag for turn off `X-Forwarded-For` ip counting
- instance overall rate limit and bust
- user rate limit and bust
- second level hacker behavior prevention (5 min of `429 Too Many Requests`)
- routing path matching before counting metrics
- exports HTTP metrics to Prometheus
