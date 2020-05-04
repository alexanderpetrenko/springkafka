# Replication
## Introduction
**Replication Application** is a replication solution that enables you to increase the availability and durability of your data by sending it from Microsoft SQL Server across multiple regions: **PostgreSQL** and **Kafka Message Broker**.

### Table Test

| Node Name                               | Datatype | Description |
| :---------------------------------------| :------- | :---------- |
|***global***                             | Object   | 
|&nbsp;&nbsp;&nbsp;`node`                                | String   | Application node name |
|&nbsp;&nbsp;&nbsp;***`logger`***                        | Object   | Defines Logging Level. Default level is INFO. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`showDateTime`      | Boolean  | On/Off the ability to display date and time.
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`logDateTimeFormat` | String   | Output format of date and time.|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`default`           | String   | Logging Level of all application. Possible values: trace, debug, warn, error, off, info.|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`jetty`             | String   | Logging Level of API server. Possible values: trace, debug, warn, error, off, info.|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`sqlserver`         | String   | Logging Level of Microsoft SQL Server. Possible values: trace, debug, warn, error, off, info.|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`postgresql`        | String   | Logging Level of PostgreSQL. Possible values: trace, debug, warn, error, off, info.|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`kafka`             | String   | Logging Level of Kafka broker. Possible values: trace, debug, warn, error, off, info.
|&nbsp;&nbsp;&nbsp;`shutdownTimeoutSec`                  | Integer  | Timeout for graceful shutdown in seconds. |
|&nbsp;&nbsp;&nbsp;`maxBatchSize`                        | Integer  | Maximal batch size of the application. |
|&nbsp;&nbsp;&nbsp;`maxBufferSize`                       | Integer  | Maximal buffer size of the application. |
|&nbsp;&nbsp;&nbsp;`waitForCDCafterInit`                 | Boolean  | On/off the pause between Initial Load and Tracking Data Changes stages. |
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

## Pandoc Table Test
+-------+-------+-------+-------+-------+-------+-------+-------+
| Node  | Dat   | D     |       |       |       |       |       |
| Name  | atype | escri |       |       |       |       |       |
|       |       | ption |       |       |       |       |       |
+=======+=======+=======+=======+=======+=======+=======+=======+
| **glo | O     |       |       |       |       |       |       |
| bal** | bject |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       | node  | S     | A     |       |       |       |       |
|       |       | tring | u     |       |       |       |       |
|       |       |       | nique |       |       |       |       |
|       |       |       | ins   |       |       |       |       |
|       |       |       | tance |       |       |       |       |
|       |       |       | name  |       |       |       |       |
|       |       |       | of    |       |       |       |       |
|       |       |       | the   |       |       |       |       |
|       |       |       | ap    |       |       |       |       |
|       |       |       | plica |       |       |       |       |
|       |       |       | tion. |       |       |       |       |
|       |       |       | It is |       |       |       |       |
|       |       |       | used  |       |       |       |       |
|       |       |       | for   |       |       |       |       |
|       |       |       | ins   |       |       |       |       |
|       |       |       | tance |       |       |       |       |
|       |       |       | iden  |       |       |       |       |
|       |       |       | tific |       |       |       |       |
|       |       |       | ation |       |       |       |       |
|       |       |       | in    |       |       |       |       |
|       |       |       | the   |       |       |       |       |
|       |       |       | table |       |       |       |       |
|       |       |       | of    |       |       |       |       |
|       |       |       | off   |       |       |       |       |
|       |       |       | sets. |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       | **log | O     | De    |       |       |       |       |
|       | ger** | bject | fines |       |       |       |       |
|       |       |       | Lo    |       |       |       |       |
|       |       |       | gging |       |       |       |       |
|       |       |       | L     |       |       |       |       |
|       |       |       | evel. |       |       |       |       |
|       |       |       | De    |       |       |       |       |
|       |       |       | fault |       |       |       |       |
|       |       |       | level |       |       |       |       |
|       |       |       | is    |       |       |       |       |
|       |       |       | INFO. |       |       |       |       |
|       |       |       |       |       |       |       |       |
|       |       |       | **Pos |       |       |       |       |
|       |       |       | sible |       |       |       |       |
|       |       |       | valu  |       |       |       |       |
|       |       |       | es:** |       |       |       |       |
|       |       |       | t     |       |       |       |       |
|       |       |       | race, |       |       |       |       |
|       |       |       | d     |       |       |       |       |
|       |       |       | ebug, |       |       |       |       |
|       |       |       | warn, |       |       |       |       |
|       |       |       | e     |       |       |       |       |
|       |       |       | rror, |       |       |       |       |
|       |       |       | off,  |       |       |       |       |
|       |       |       | info  |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | de    | S     | Lo    |       |       |       |
|       |       | fault | tring | gging |       |       |       |
|       |       |       |       | Level |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | e     |       |       |       |
|       |       |       |       | ntire |       |       |       |
|       |       |       |       | ap    |       |       |       |
|       |       |       |       | plica |       |       |       |
|       |       |       |       | tion. |       |       |       |
|       |       |       |       |       |       |       |       |
|       |       |       |       | **De  |       |       |       |
|       |       |       |       | fault |       |       |       |
|       |       |       |       | va    |       |       |       |
|       |       |       |       | lue** |       |       |       |
|       |       |       |       | is    |       |       |       |
|       |       |       |       | INFO. |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | jetty | S     | Lo    |       |       |       |
|       |       |       | tring | gging |       |       |       |
|       |       |       |       | Level |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | emb   |       |       |       |
|       |       |       |       | edded |       |       |       |
|       |       |       |       | web   |       |       |       |
|       |       |       |       | se    |       |       |       |
|       |       |       |       | rver. |       |       |       |
|       |       |       |       |       |       |       |       |
|       |       |       |       | The   |       |       |       |
|       |       |       |       | **De  |       |       |       |
|       |       |       |       | fault |       |       |       |
|       |       |       |       | va    |       |       |       |
|       |       |       |       | lue** |       |       |       |
|       |       |       |       | is a  |       |       |       |
|       |       |       |       | value |       |       |       |
|       |       |       |       | from  |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | *     |       |       |       |
|       |       |       |       | *defa |       |       |       |
|       |       |       |       | ult** |       |       |       |
|       |       |       |       | node  |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | cu    |       |       |       |
|       |       |       |       | rrent |       |       |       |
|       |       |       |       | sec   |       |       |       |
|       |       |       |       | tion. |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | sqls  | S     | Lo    |       |       |       |
|       |       | erver | tring | gging |       |       |       |
|       |       |       |       | Level |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | Micr  |       |       |       |
|       |       |       |       | osoft |       |       |       |
|       |       |       |       | SQL   |       |       |       |
|       |       |       |       | Se    |       |       |       |
|       |       |       |       | rver. |       |       |       |
|       |       |       |       |       |       |       |       |
|       |       |       |       | The   |       |       |       |
|       |       |       |       | **De  |       |       |       |
|       |       |       |       | fault |       |       |       |
|       |       |       |       | va    |       |       |       |
|       |       |       |       | lue** |       |       |       |
|       |       |       |       | is a  |       |       |       |
|       |       |       |       | value |       |       |       |
|       |       |       |       | from  |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | *     |       |       |       |
|       |       |       |       | *defa |       |       |       |
|       |       |       |       | ult** |       |       |       |
|       |       |       |       | node  |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | cu    |       |       |       |
|       |       |       |       | rrent |       |       |       |
|       |       |       |       | sec   |       |       |       |
|       |       |       |       | tion. |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | postg | S     | Lo    |       |       |       |
|       |       | resql | tring | gging |       |       |       |
|       |       |       |       | Level |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | P     |       |       |       |
|       |       |       |       | ostgr |       |       |       |
|       |       |       |       | eSQL. |       |       |       |
|       |       |       |       |       |       |       |       |
|       |       |       |       | The   |       |       |       |
|       |       |       |       | **De  |       |       |       |
|       |       |       |       | fault |       |       |       |
|       |       |       |       | va    |       |       |       |
|       |       |       |       | lue** |       |       |       |
|       |       |       |       | is a  |       |       |       |
|       |       |       |       | value |       |       |       |
|       |       |       |       | from  |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | *     |       |       |       |
|       |       |       |       | *defa |       |       |       |
|       |       |       |       | ult** |       |       |       |
|       |       |       |       | node  |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | cu    |       |       |       |
|       |       |       |       | rrent |       |       |       |
|       |       |       |       | sec   |       |       |       |
|       |       |       |       | tion. |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | kafka | S     | Lo    |       |       |       |
|       |       |       | tring | gging |       |       |       |
|       |       |       |       | Level |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | Kafka |       |       |       |
|       |       |       |       | br    |       |       |       |
|       |       |       |       | oker. |       |       |       |
|       |       |       |       |       |       |       |       |
|       |       |       |       | The   |       |       |       |
|       |       |       |       | **De  |       |       |       |
|       |       |       |       | fault |       |       |       |
|       |       |       |       | va    |       |       |       |
|       |       |       |       | lue** |       |       |       |
|       |       |       |       | is a  |       |       |       |
|       |       |       |       | value |       |       |       |
|       |       |       |       | from  |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | *     |       |       |       |
|       |       |       |       | *defa |       |       |       |
|       |       |       |       | ult** |       |       |       |
|       |       |       |       | node  |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | the   |       |       |       |
|       |       |       |       | cu    |       |       |       |
|       |       |       |       | rrent |       |       |       |
|       |       |       |       | sec   |       |       |       |
|       |       |       |       | tion. |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | sh    | Bo    | O     |       |       |       |
|       |       | owDat | olean | n/Off |       |       |       |
|       |       | eTime |       | the   |       |       |       |
|       |       |       |       | ab    |       |       |       |
|       |       |       |       | ility |       |       |       |
|       |       |       |       | to    |       |       |       |
|       |       |       |       | di    |       |       |       |
|       |       |       |       | splay |       |       |       |
|       |       |       |       | date  |       |       |       |
|       |       |       |       | and   |       |       |       |
|       |       |       |       | time. |       |       |       |
|       |       |       |       |       |       |       |       |
|       |       |       |       | **De  |       |       |       |
|       |       |       |       | fault |       |       |       |
|       |       |       |       | val   |       |       |       |
|       |       |       |       | ue:** |       |       |       |
|       |       |       |       | true  |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | lo    | S     | O     |       |       |       |
|       |       | gDate | tring | utput |       |       |       |
|       |       | TimeF |       | f     |       |       |       |
|       |       | ormat |       | ormat |       |       |       |
|       |       |       |       | of    |       |       |       |
|       |       |       |       | date  |       |       |       |
|       |       |       |       | and   |       |       |       |
|       |       |       |       | time. |       |       |       |
|       |       |       |       |       |       |       |       |
|       |       |       |       | **De  |       |       |       |
|       |       |       |       | fault |       |       |       |
|       |       |       |       | val   |       |       |       |
|       |       |       |       | ue:** |       |       |       |
|       |       |       |       | \"    |       |       |       |
|       |       |       |       | yyyy- |       |       |       |
|       |       |       |       | MM-dd |       |       |       |
|       |       |       |       | HH:   |       |       |       |
|       |       |       |       | mm:ss |       |       |       |
|       |       |       |       | z\"   |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       | shu   | In    | Ti    |       |       |       |       |
|       | tdown | teger | meout |       |       |       |       |
|       | Timeo |       | for   |       |       |       |       |
|       | utSec |       | gra   |       |       |       |       |
|       |       |       | ceful |       |       |       |       |
|       |       |       | shu   |       |       |       |       |
|       |       |       | tdown |       |       |       |       |
|       |       |       | in    |       |       |       |       |
|       |       |       | sec   |       |       |       |       |
|       |       |       | onds. |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       | ma    | In    | Ma    |       |       |       |       |
|       | xBatc | teger | ximal |       |       |       |       |
|       | hSize |       | batch |       |       |       |       |
|       |       |       | size  |       |       |       |       |
|       |       |       | of    |       |       |       |       |
|       |       |       | the   |       |       |       |       |
|       |       |       | ap    |       |       |       |       |
|       |       |       | plica |       |       |       |       |
|       |       |       | tion. |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       | max   | In    | Ma    |       |       |       |       |
|       | Buffe | teger | ximal |       |       |       |       |
|       | rSize |       | b     |       |       |       |       |
|       |       |       | uffer |       |       |       |       |
|       |       |       | size  |       |       |       |       |
|       |       |       | of    |       |       |       |       |
|       |       |       | the   |       |       |       |       |
|       |       |       | ap    |       |       |       |       |
|       |       |       | plica |       |       |       |       |
|       |       |       | tion. |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       | wait  | Bo    | O     |       |       |       |       |
|       | ForCD | olean | n/off |       |       |       |       |
|       | Cafte |       | the   |       |       |       |       |
|       | rInit |       | pause |       |       |       |       |
|       |       |       | be    |       |       |       |       |
|       |       |       | tween |       |       |       |       |
|       |       |       | In    |       |       |       |       |
|       |       |       | itial |       |       |       |       |
|       |       |       | Load  |       |       |       |       |
|       |       |       | and   |       |       |       |       |
|       |       |       | Tra   |       |       |       |       |
|       |       |       | cking |       |       |       |       |
|       |       |       | Data  |       |       |       |       |
|       |       |       | Ch    |       |       |       |       |
|       |       |       | anges |       |       |       |       |
|       |       |       | st    |       |       |       |       |
|       |       |       | ages. |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       | **    | O     |       |       |       |       |       |
|       | defau | bject |       |       |       |       |       |
|       | lts** |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | **con | O     |       |       |       |       |
|       |       | necti | bject |       |       |       |       |
|       |       | ons** |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | query | Bo    |       |       |       |
|       |       |       | Debug | olean |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | qu    | In    |       |       |       |
|       |       |       | eryTi | teger |       |       |       |
|       |       |       | meout |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | maxC  | In    | Set   |       |       |
|       |       |       | onnec | teger | the   |       |       |
|       |       |       | tions |       | ma    |       |       |
|       |       |       |       |       | ximum |       |       |
|       |       |       |       |       | n     |       |       |
|       |       |       |       |       | umber |       |       |
|       |       |       |       |       | of    |       |       |
|       |       |       |       |       | c     |       |       |
|       |       |       |       |       | onnec |       |       |
|       |       |       |       |       | tions |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | **sou | O     |       |       |       |       |
|       |       | rce** | bject |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | mode  | S     | *Pos  |       |       |
|       |       |       |       | tring | sible |       |       |
|       |       |       |       |       | val   |       |       |
|       |       |       |       |       | ues:* |       |       |
|       |       |       |       |       | RE    |       |       |
|       |       |       |       |       | PLICA |       |       |
|       |       |       |       |       | TION, |       |       |
|       |       |       |       |       | DBO,  |       |       |
|       |       |       |       |       | CDC   |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | conne | S     | The   |       |       |
|       |       |       | ction | tring | key   |       |       |
|       |       |       |       |       | of    |       |       |
|       |       |       |       |       | the   |       |       |
|       |       |       |       |       | s     |       |       |
|       |       |       |       |       | ource |       |       |
|       |       |       |       |       | d     |       |       |
|       |       |       |       |       | atast |       |       |
|       |       |       |       |       | orage |       |       |
|       |       |       |       |       | conne |       |       |
|       |       |       |       |       | ction |       |       |
|       |       |       |       |       | (de   |       |       |
|       |       |       |       |       | fines |       |       |
|       |       |       |       |       | in    |       |       |
|       |       |       |       |       | *dat  |       |       |
|       |       |       |       |       | astor |       |       |
|       |       |       |       |       | ages* |       |       |
|       |       |       |       |       | node) |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | sna   | S     | The   |       |       |
|       |       |       | pshot | tring | key   |       |       |
|       |       |       |       |       | of    |       |       |
|       |       |       |       |       | the   |       |       |
|       |       |       |       |       | sna   |       |       |
|       |       |       |       |       | pshot |       |       |
|       |       |       |       |       | conne |       |       |
|       |       |       |       |       | ction |       |       |
|       |       |       |       |       | of    |       |       |
|       |       |       |       |       | the   |       |       |
|       |       |       |       |       | s     |       |       |
|       |       |       |       |       | ource |       |       |
|       |       |       |       |       | d     |       |       |
|       |       |       |       |       | atast |       |       |
|       |       |       |       |       | orage |       |       |
|       |       |       |       |       | (de   |       |       |
|       |       |       |       |       | fines |       |       |
|       |       |       |       |       | in    |       |       |
|       |       |       |       |       | *dat  |       |       |
|       |       |       |       |       | astor |       |       |
|       |       |       |       |       | ages* |       |       |
|       |       |       |       |       | node) |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | buffe | In    | Sets  |       |       |
|       |       |       | rSize | teger | the   |       |       |
|       |       |       |       |       | size  |       |       |
|       |       |       |       |       | of a  |       |       |
|       |       |       |       |       | b     |       |       |
|       |       |       |       |       | uffer |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | **    | O     |       |       |       |
|       |       |       | dbo** | bject |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | s     | S     |       |       |
|       |       |       |       | chema | tring |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | save  | Bo    |       |       |
|       |       |       |       | SkipO | olean |       |       |
|       |       |       |       | ffset |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | ign   | Bo    |       |       |
|       |       |       |       | oreDu | olean |       |       |
|       |       |       |       | plica |       |       |       |
|       |       |       |       | teKey |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | sc    | Bo    |       |       |
|       |       |       |       | rollI | olean |       |       |
|       |       |       |       | nsens |       |       |       |
|       |       |       |       | itive |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | initi | S     | *Pos  |       |
|       |       |       |       | alStr | tring | sible |       |
|       |       |       |       | ategy |       | val   |       |
|       |       |       |       |       |       | ues:* |       |
|       |       |       |       |       |       | NONE, |       |
|       |       |       |       |       |       | IN    |       |
|       |       |       |       |       |       | CREME |       |
|       |       |       |       |       |       | NTAL, |       |
|       |       |       |       |       |       | TIMES |       |
|       |       |       |       |       |       | TAMP, |       |
|       |       |       |       |       |       | U     |       |
|       |       |       |       |       |       | NIQUE |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | **    | O     |       |       |       |
|       |       |       | cdc** | bject |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | s     | S     |       |       |
|       |       |       |       | chema | tring |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | int   | In    |       |       |
|       |       |       |       | erval | teger |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | epoch | Bo    |       |       |
|       |       |       |       |       | olean |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | **des | O     |       |       |       |       |
|       |       | tinat | bject |       |       |       |       |
|       |       | ion** |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | **po  | O     |       |       |       |
|       |       |       | stgre | bject |       |       |       |
|       |       |       | sql** |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | s     | S     |       |       |
|       |       |       |       | chema | tring |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | conne | S     | The   |       |
|       |       |       |       | ction | tring | key   |       |
|       |       |       |       |       |       | of    |       |
|       |       |       |       |       |       | the   |       |
|       |       |       |       |       |       | t     |       |
|       |       |       |       |       |       | arget |       |
|       |       |       |       |       |       | d     |       |
|       |       |       |       |       |       | atast |       |
|       |       |       |       |       |       | orage |       |
|       |       |       |       |       |       | conne |       |
|       |       |       |       |       |       | ction |       |
|       |       |       |       |       |       | (de   |       |
|       |       |       |       |       |       | fines |       |
|       |       |       |       |       |       | in    |       |
|       |       |       |       |       |       | *dat  |       |
|       |       |       |       |       |       | astor |       |
|       |       |       |       |       |       | ages* |       |
|       |       |       |       |       |       | node) |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | batc  | In    | Sets  |       |
|       |       |       |       | hSize | teger | the   |       |
|       |       |       |       |       |       | size  |       |
|       |       |       |       |       |       | of a  |       |
|       |       |       |       |       |       | batch |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       | **ka  | O     |       |       |       |
|       |       |       | fka** | bject |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | conne | S     | The   |       |
|       |       |       |       | ction | tring | key   |       |
|       |       |       |       |       |       | of    |       |
|       |       |       |       |       |       | the   |       |
|       |       |       |       |       |       | t     |       |
|       |       |       |       |       |       | arget |       |
|       |       |       |       |       |       | d     |       |
|       |       |       |       |       |       | atast |       |
|       |       |       |       |       |       | orage |       |
|       |       |       |       |       |       | conne |       |
|       |       |       |       |       |       | ction |       |
|       |       |       |       |       |       | (de   |       |
|       |       |       |       |       |       | fines |       |
|       |       |       |       |       |       | in    |       |
|       |       |       |       |       |       | *dat  |       |
|       |       |       |       |       |       | astor |       |
|       |       |       |       |       |       | ages* |       |
|       |       |       |       |       |       | node) |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | trans | S     |       |       |
|       |       |       |       | actio | tring |       |       |
|       |       |       |       | nalId |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | tran  | S     |       |       |
|       |       |       |       | sacti | tring |       |       |
|       |       |       |       | onalP |       |       |       |
|       |       |       |       | refix |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | batc  | In    | Sets  |       |
|       |       |       |       | hSize | teger | the   |       |
|       |       |       |       |       |       | size  |       |
|       |       |       |       |       |       | of a  |       |
|       |       |       |       |       |       | batch |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       | *     | O     |       |       |
|       |       |       |       | *mess | bject |       |       |
|       |       |       |       | age** |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       |       | meta  | S     |       |
|       |       |       |       |       |       | tring |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       |       | data  | S     |       |
|       |       |       |       |       |       | tring |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       |       | b     | S     |       |
|       |       |       |       |       | efore | tring |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       |       | type  | S     | *Pos  |
|       |       |       |       |       |       | tring | sible |
|       |       |       |       |       |       |       | val   |
|       |       |       |       |       |       |       | ues:* |
|       |       |       |       |       |       |       | MAP,  |
|       |       |       |       |       |       |       | JSON  |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       |       | us    | Bo    |       |
|       |       |       |       |       | eMeta | olean |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       |       | us    | Bo    |       |
|       |       |       |       |       | eData | olean |       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       |       | useB  | Bo    |       |
|       |       |       |       |       | efore | olean |       |
+-------+-------+-------+-------+-------+-------+-------+-------+