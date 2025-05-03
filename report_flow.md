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
    G --> cgi-bin/reports-metadata.cgi
    cgi-bin/reports-metadata.cgi --> L(CPAN::Testers::WWW
          ::Reports::Query::Reports)
    L --> M(andl-cpan-tools/
          refill-cpanstatsdb.pl)
    M --> FAST2-MATRIX
```
