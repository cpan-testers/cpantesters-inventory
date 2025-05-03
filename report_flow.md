This flowchart describes where a test report goes. It's most easily edited with https://mermaid.live

```mermaid
flowchart TD
    A[CPAN client] -->|Generates Test Report| B(Metabase - Ingest)
    B -->|Enqueues| C(Backend - Minion)
    C -->|Processes| D[Stats Mysql DB]
    D --> F[API Mojo]
    D --> G[Web Mojo]
```
