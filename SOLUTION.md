# REST vs. gRPC Performance Comparison

## Performance Results

The table below shows the average execution time per operation in milliseconds (ms) for REST and gRPC across three network configurations.

| Method | Local (ms) | Same-Zone (ms) | Different Region (ms) |
|---|---:|---:|---:|
| REST add | 2.86 | 3.43 | 447.52 |
| gRPC add | 0.90 | 1.16 | 161.08 |
| REST rawImage | 5.75 | 7.99 | 1344.93 |
| gRPC rawImage | 18.09 | 13.78 | 210.04 |
| REST dotProduct | 3.31 | 4.11 | 329.04 |
| gRPC dotProduct | 0.96 | 1.39 | 179.25 |
| REST jsonImage | 28.90 | 30.90 | 1478.14 |
| gRPC jsonImage | 31.74 | 25.28 | 183.25 |


## Observations

The results show that gRPC generally performs better than REST, particularly when the client and server are in different regions. For local and same zone communication, the performance difference is relatively small, with REST performing better for some image operations. However, cross region latency significantly increases execution time for both protocols, especially REST. One major reason is that the REST implementation establishes a new TCP connection for each request, while gRPC reuses a persistent connection across multiple requests. This connection reuse reduces overhead and makes gRPC more efficient when network latency is high. Overall, the results demonstrate that network latency plays a major role in RPC performance and that gRPC provides a significant advantage for communication across geographically distant servers.
