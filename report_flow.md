This flowchart describes where a test report goes. It's most easily edited with https://mermaid.live

```mermaid
flowchart TD
    A[CPAN client]
      --> inurl[metabase.cpantesters.org
          /api/v1/]
      --> B(Metabase - Ingest)
      -->|Enqueues| C(Backend - Minion)
    C -->|Processes| D(Stats Mysql DB)
    D --> F(API Mojo)
    D --> G(Web Mojo)

    B --> taillog(metabase.cpantesters.org/
                  tail/log.txt) --> M1[(FAST-MATRIX)]
    
    G --> jrep(cpantesters.org/
               show/DBIx-Class.json)
      --> M2[(MATRIX)]

    G --> repmeta(cpantesters.org/cgi-bin
        /reports-metadata.cgi
        virtual route)
      --> qreports(CPAN::Testers::WWW
          ::Reports::Query::Reports)
      --> refill(andk-cpan-tools/
          refill-cpanstatsdb.pl)
      --> M3[(FAST2-MATRIX)]
    
    B --> H
    subgraph new design
        H(Tag Extractor) --> I(New Stats DB)
        I --> J(New API)
        I --> K(New Web)
    end
```
