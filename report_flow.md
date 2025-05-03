This flowchart describes where a test report goes. It's most easily edited with https://mermaid.live

```mermaid
flowchart TD
    A[CPAN client] -->|Generates Test Report| B(Metabase - Ingest)
    B -->|Enqueues| C(Backend - Minion)
    C -->|Processes| D(Stats Mysql DB)
    D --> F(API Mojo)
    D --> G(Web Mojo)
    B -->|NEW DESIGN| H(Tag Extractor)
    subgraph new design
    H --> I(New Stats DB)
    I --> J(New API)
    I --> K(New Web)
    end
    G -->|provides report JSON| MATRIX
    B -->|log tail| FAST-MATRIX
    D -->   |CPAN::Testers::WWW::
            Reports::Query::Reports
            or CPAN::Testers::WWW::
            Reports::Query::Report| FAST2-MATRIX
```
