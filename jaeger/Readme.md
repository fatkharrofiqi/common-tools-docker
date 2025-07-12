# 📝 Flow
```
[ Your App ]
   |
   | (sends spans via OTLP gRPC: **4317** or HTTP: **4318**)
   v
[ OpenTelemetry Collector ]
   | Receivers:
   |   - OTLP gRPC (**4317**)
   |   - OTLP HTTP (**4318**)
   |   - Jaeger Thrift gRPC (**14250**)
   |   - Jaeger Thrift HTTP (**14268**)
   |
   | Processors:
   |   - batch, transform, filter, etc.
   |
   | Exporters:
   |   - Jaeger exporter (sends to jaeger-collector **14250** gRPC)
   v
[ Jaeger Collector ]
   | Receives from:
   |   - otel-collector (**14250** gRPC)
   |   - apps (optional direct ingestion)
   |
   | Stores traces into:
   |   - Storage backend (Cassandra default port: **9042**)
   v
[ Jaeger Storage Backend ]
   |
   v
[ Jaeger Query Service ]
   | Exposes UI on:
   |   - **16686** (Jaeger UI)
   |
   v
[ Jaeger UI ]
   | Developers access via browser:
   |   - http://localhost:16686 or domain
```
   
# 📝 Key Ports Summary
| Component | Purpose | Port |
| ------ | ------ | ------ |
| Your App → otel-collector | OTLP gRPC | 4317 |
| Your App → otel-collector | OTLP HTTP | 4318 |
| otel-collector → jaeger-collector | Jaeger gRPC exporter | 14250 |
| otel-collector → jaeger-collector | Jaeger HTTP exporter | 14268 |
| jaeger-collector → storage | Cassandra | 9042 |
| jaeger-query (UI)	| Web UI | 16686 |

# 🚀 End-to-End Flow Example
1. App sends trace via OTLP gRPC (4317) ➔ otel-collector.

2. otel-collector processes (batch, transform) ➔ exports via Jaeger exporter to jaeger-collector (14250 gRPC).

3. jaeger-collector writes data to Cassandra (9042).

4. jaeger-query queries Cassandra and displays results on UI (16686).
