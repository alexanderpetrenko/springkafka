# WAG / DIH SQL Replication
## Introduction
**DIH SQL Replication Application** is a replication solution that enables you to increase the availability and durability of your data by sending it from Microsoft SQL Server across multiple regions: **PostgreSQL** and **Kafka Message Broker**.




```
global
├── node ____________________________│ String  │ Application node name
├── logger __________________________│ Object  │ Defines Logging Level. Default level is INFO.
│   ├── showDateTime ________________│ Boolean │ On/Off the ability to display date and time.
│   ├── logDateTimeFormat ___________│ String  │ Output format of date and time.
│   ├── default _____________________│ String  │ Logging Level of all application. Possible values: trace, debug, warn, error, off, info.
│   ├── jetty _______________________│ String  │ Logging Level of API server. Possible values: trace, debug, warn, error, off, info.
│   ├── sqlserver ___________________│ String  │ Logging Level of Microsoft SQL Server. Possible values: trace, debug, warn, error, off, info.
│   ├── postgresql __________________│ String  │ Logging Level of PostgreSQL. Possible values: trace, debug, warn, error, off, info.
│   └── kafka _______________________│ String  │ Logging Level of Kafka broker. Possible values: trace, debug, warn, error, off, info.
├── shutdownTimeoutSec ______________│ Integer │ Timeout for graceful shutdown in seconds.
├── maxBatchSize ____________________│ Integer │ Maximal batch size of the application.
├── maxBufferSize ___________________│ Integer │ Maximal buffer size of the application.
├── waitForCDCafterInit _____________│ Boolean │ On/off the pause between Initial Load and Tracking Data Changes stages.
└── defaults ________________________│ Object  │
    ├── connections _________________│ Object  │
    │   ├── queryDebug ______________│ Boolean │
    │   ├── queryTimeout ____________│ Integer │
    │   └── maxConnections __________│ Integer │
    ├── source ______________________│ Object  │
    │   ├── mode ____________________│ String  │ Possible values: REPLICATION, DBO, CDC
    │   ├── connection ______________│ String  │
    │   ├── snapshot ________________│ String  │
    │   ├── bufferSize ______________│ Integer │
    │   ├── dbo _____________________│ Object  │
    │   │   ├── schema ______________│ String  │
    │   │   ├── saveSkipOffset ______│ Boolean │
    │   │   ├── ignoreDuplicateKey __│ Boolean │
    │   │   ├── scrollInsensitive ___│ Boolean │
    │   │   └── scrollInsensitive ___│ String  │ Possible values: NONE, INCREMENTAL, TIMESTAMP, UNIQUE
    │   └── cdc _____________________│ Object  │
    │       ├── schema ______________│ String  │
    │       ├── interval ____________│ Integer │
    │       └── epoch _______________│ Boolean │
    └── destination _________________│ Object  │
        ├── postgresql ______________│ Object  │
        │   ├── schema ______________│ String  │
        │   ├── connection __________│ String  │
        │   └── batchSize ___________│ Integer │
        └── kafka ___________________│ Object  │
            ├── connection __________│ String  │
            ├── transactionalId _____│ Integer │
            ├── transactionalPrefix _│ String  │
            ├── batchSize ___________│ Integer │
            └── message _____________│ Object  │
                ├── meta ____________│ String  │
                ├── data ____________│ String  │
                ├── before __________│ String  │
                ├── type ____________│ String  │
                ├── useMeta _________│ Boolean │
                ├── useData _________│ Boolean │
                └── useBefore _______│ Boolean │
```
Table Test