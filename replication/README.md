# Replication
## Introduction
**Replication Application** is a replication solution that enables you to increase the availability and durability of your data by sending it from Microsoft SQL Server across multiple regions: **PostgreSQL** and **Kafka Message Broker**.

### Table Test

| Node Name                               | Datatype | Description |
| :---------------------------------------| :------- | :---------- |
|***global***                             | Object   | |
|&nbsp;&nbsp;&nbsp;node                   | String   | A unique instance name of the application.<br>It is used for instance identification in the table of offsets. |
|&nbsp;&nbsp;&nbsp;***logger***                        | Object   | Defines Logging Level. Default level is INFO.<br>Possible values: trace, debug, warn, error, off, info |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;default           | String   | Logging Level of all application.<br>***Default value*** is INFO. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;jetty             | String   | Logging Level of API server.<br>The ***Default value*** is a value from the ***default*** node of the current section. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sqlserver         | String   | Logging Level of Microsoft SQL Server.<br>The ***Default value*** is a value from the ***default*** node of the current section. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;postgresql        | String   | Logging Level of PostgreSQL.<br>The ***Default value*** is a value from the ***default*** node of the current section.|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;kafka             | String   | Logging Level of Kafka broker.<br>The ***Default value*** is a value from the ***default*** node of the current section. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;showDateTime      | Boolean  | On/Off the ability to display date and time.<br>***Default value:*** true |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;logDateTimeFormat | String   | Output format of date and time.<br>***Default value:*** "yyyy-MM-dd HH:mm:ss z" |
|&nbsp;&nbsp;&nbsp;shutdownTimeoutSec                  | Integer  | Timeout for graceful shutdown in seconds. |
|&nbsp;&nbsp;&nbsp;maxBatchSize                        | Integer  | Maximal batch size of the application. |
|&nbsp;&nbsp;&nbsp;maxBufferSize                       | Integer  | Maximal buffer size of the application. |
|&nbsp;&nbsp;&nbsp;waitForCDCafterInit                 | Boolean  | On/off the pause between Initial Load and Tracking Data Changes stages. |
|└>***`defaults`***                       | Object   | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├>***`connections`*** | Object   | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`queryDebug`     | Boolean | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`queryTimeout`   | Integer | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;└─`maxConnections` | Integer | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├>***`source`*** | Object   | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`mode`       | String  | Possible values: REPLICATION, DBO, CDC |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`connection` | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`snapshot`   | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`bufferSize` | Integer | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├>***`dbo`*** | Object  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`schema`             | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`saveSkipOffset`     | Boolean | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`ignoreDuplicateKey` | Boolean | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`scrollInsensitive`  | Boolean | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;└─`initialStrategy`    | String  | Possible values: NONE, INCREMENTAL, TIMESTAMP, UNIQUE |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;└>***`cdc`*** | Object  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`schema`   | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`interval` | Integer | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─`epoch`    | Boolean | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└>***`destination`*** | Object   | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├>***`postgresql`*** | Object  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`schema`     | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├─`connection` | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;└─`batchSize`  | Integer | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└>***`kafka`***      | Object  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`connection`          | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`transactionalId`     | Integer | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`transactionalPrefix` | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`batchSize`           | Integer | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└>***`message`*** | Object | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`meta`      | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`data`      | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`before`    | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`type`      | String  | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`useMeta`   | Boolean | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├─`useData`   | Boolean | |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└─`useBefore` | Boolean | |