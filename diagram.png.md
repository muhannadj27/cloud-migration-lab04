graph TD
    User[Users / Internet]

    subgraph Azure_Cloud [Azure Cloud]
        LB[Load Balancer]

        subgraph AKS [AKS Cluster]
            Pod1[Node.js Pod]
            Pod2[Node.js Pod]
            Pod3[Node.js Pod]
        end

        DB[(Azure SQL Database)]
    end

    User --> LB
    LB --> Pod1
    LB --> Pod2
    LB --> Pod3
    Pod1 --> DB
    Pod2 --> DB
    Pod3 --> DB

    %% Styling
    classDef azure fill:#0078d4,stroke:#005a9e,color:#fff
    classDef database fill:#f2f2f2,stroke:#333,stroke-width:2px

    class LB,Pod1,Pod2,Pod3 azure
    class DB database
