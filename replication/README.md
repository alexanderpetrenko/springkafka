<style>
   ul.tree, ul.tree ul {
    list-style: none;
     margin: 0;
     padding: 0;
   } 
   ul.tree ul {
     margin-left: 10px;
   }
   ul.tree li {
     margin: 0;
     padding: 0 7px;
     line-height: 20px;
     color: #369;
     font-weight: bold;
     border-left:1px solid rgb(100,100,100);

   }
   ul.tree li:last-child {
       border-left:none;
   }
   ul.tree li:before {
      position:relative;
      top:-0.3em;
      height:1em;
      width:12px;
      color:white;
      border-bottom:1px solid rgb(100,100,100);
      content:"";
      display:inline-block;
      left:-7px;
   }
   ul.tree li:last-child:before {
      border-left:1px solid rgb(100,100,100);   
   }
</style>

# WAG / DIH SQL Replication
## Introduction
**DIH SQL Replication Application** is a replication solution that enables you to increase the availability and durability of your data by sending it from Microsoft SQL Server across multiple regions: **PostgreSQL** and **Kafka Message Broker**.




````
global
├── node ____________________________│ String  │ Application node name
├─> logger __________________________│ Object  │ Defines Logging Level. Default level is INFO.
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
└─> defaults ________________________│ Object  │
    ├─> connections _________________│ Object  │
    │   ├── queryDebug ______________│ Boolean │
    │   ├── queryTimeout ____________│ Integer │
    │   └── maxConnections __________│ Integer │
    ├─> source ______________________│ Object  │
    │   ├── mode ____________________│ String  │ Possible values: REPLICATION, DBO, CDC
    │   ├── connection ______________│ String  │
    │   ├── snapshot ________________│ String  │
    │   ├── bufferSize ______________│ Integer │
    │   ├─> dbo _____________________│ Object  │
    │   │   ├── schema ______________│ String  │
    │   │   ├── saveSkipOffset ______│ Boolean │
    │   │   ├── ignoreDuplicateKey __│ Boolean │
    │   │   ├── scrollInsensitive ___│ Boolean │
    │   │   └── scrollInsensitive ___│ String  │ Possible values: NONE, INCREMENTAL, TIMESTAMP, UNIQUE
    │   └─> cdc _____________________│ Object  │
    │       ├── schema ______________│ String  │
    │       ├── interval ____________│ Integer │
    │       └── epoch _______________│ Boolean │
    └─> destination _________________│ Object  │
        ├─> postgresql ______________│ Object  │
        │   ├── schema ______________│ String  │
        │   ├── connection __________│ String  │
        │   └── batchSize ___________│ Integer │
        └─> kafka ___________________│ Object  │
            ├── connection __________│ String  │
            ├── transactionalId _____│ Integer │
            ├── transactionalPrefix _│ String  │
            ├── batchSize ___________│ Integer │
            └─> message _____________│ Object  │
                ├── meta ____________│ String  │
                ├── data ____________│ String  │
                ├── before __________│ String  │
                ├── type ____________│ String  │
                ├── useMeta _________│ Boolean │
                ├── useData _________│ Boolean │
                └── useBefore _______│ Boolean │
````

### Table Test

| Node Name                               | Datatype | Description |
| :---------------------------------------| :------- | :---------- |
|global                                   | Object   | 
|├─`node`                                 | String   | Application node name |
|├>`logger`                               | Object   | Defines Logging Level. Default level is INFO. |
|│&nbsp;&nbsp;&nbsp;├─`showDateTime`      | Boolean  | On/Off the ability to display date and time.
|│&nbsp;&nbsp;&nbsp;├─`logDateTimeFormat` | String   | Output format of date and time.|
|│&nbsp;&nbsp;&nbsp;├─`default`           | String   | Logging Level of all application. Possible values: trace, debug, warn, error, off, info.|
|│&nbsp;&nbsp;&nbsp;├─`jetty`             | String   | Logging Level of API server. Possible values: trace, debug, warn, error, off, info.|
|│&nbsp;&nbsp;&nbsp;├─`sqlserver`         | String   | Logging Level of Microsoft SQL Server. Possible values: trace, debug, warn, error, off, info.|
|│&nbsp;&nbsp;&nbsp;├─`postgresql`        | String   | Logging Level of PostgreSQL. Possible values: trace, debug, warn, error, off, info.|
|│&nbsp;&nbsp;&nbsp;└─`kafka`             | String   | Logging Level of Kafka broker. Possible values: trace, debug, warn, error, off, info.
|├─`shutdownTimeoutSec`                   | Integer  | Timeout for graceful shutdown in seconds. |
|├─`maxBatchSize`                         | Integer  | Maximal batch size of the application. |
|├─`maxBufferSize`                        | Integer  | Maximal buffer size of the application. |
|├─`waitForCDCafterInit`                  | Boolean  | On/off the pause between Initial Load and Tracking Data Changes stages. |
|└>`defaults`                             | Object   | |
|&nbsp;&nbsp;&nbsp;├>`connections`        | Object   | |
|&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`queryDebug`     | Boolean | |
|&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`queryTimeout`   | Integer | |
|&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;└─`maxConnections` | Integer | |


<ul class="tree">
    <li>Animals
     <ul>
      <li>Birds</li>
      <li>Mammals
       <ul>
        <li>Elephant</li>
        <li class="last">Mouse</li>
       </ul>
      </li>
      <li class="last">Reptiles</li>
     </ul>
    </li>
    <li class="last">Plants
     <ul>
      <li>Flowers
       <ul>
        <li>Rose</li>
        <li class="last">Tulip</li>
       </ul>
      </li>
      <li class="last">Trees</li>
     </ul>
    </li>
   </ul>