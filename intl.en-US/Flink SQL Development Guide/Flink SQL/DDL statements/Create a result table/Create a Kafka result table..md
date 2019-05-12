# Create a Kafka result table. {#concept_88918_zh .concept}

This topic describes how to create a Kafka result table in Realtime Compute.

**Note:** This topic applies only to Realtime Compute deployed in exclusive mode.

## DDL definition {#section_j1v_npg_cgb .section}

The DDL statement used to create a Kafka result table is defined as follows:

```language-sql
create table sink_kafka (
    messageKey VARBINARY,
    `message` VARBINARY,
    PRIMARY KEY (messageKey)
) with (
    type = 'kafka010',
    topic = '<yourTopicName>',
    bootstrap.servers = '<yourServerAddress>'
);
```

**Note:** 

-   You must explicitly declare the PRIMARY KEY \(messageKey\) when you create a Kafka result table.
-   Only Realtime Compute V2.2.6 and later support displaying metric information such as TPS and RPS of Alibaba Cloud Kafka or your self-built Kafka.

## WITH parameters {#section_dj3_bqg_cgb .section}

General configuration

|Name|Description|Remarks|
|----|-----------|-------|
|type|The Kafka version name.|Required. Valid values: Kafka08, Kafka09, Kafka010, and Kafka011. For the version mapping, see **Mapping between Kafka version names and version numbers**.|
|topic|The topic to be written.|The topic name.|

-   Required configuration
    -   Required configuration for Kafka08

        |Name|Description|Remarks|
        |----|-----------|-------|
        |zookeeper.connect|The ZooKeeper URL.|The ZooKeeper connection ID.|

    -   Required configuration for Kafka09, Kafka010, and Kafka011

        |Name|Description|Remarks|
        |----|-----------|-------|
        |bootstrap.servers|The Kafka cluster address.|None|

-   Optional configuration

    -   `consumer.id`
    -   `socket.timeout.ms`
    -   `fetch.message.max.bytes`
    -   `num.consumer.fetchers`
    -   `auto.commit.enable`
    -   `auto.commit.interval.ms`
    -   `queued.max.message.chunks`
    -   `rebalance.max.retries`
    -   `fetch.min.bytes`
    -   `fetch.wait.max.ms`
    -   `rebalance.backoff.ms`
    -   `refresh.leader.backoff.ms`
    -   `auto.offset.reset`
    -   `consumer.timeout.ms`
    -   `exclude.internal.topics`
    -   `partition.assignment.strategy`
    -   `client.id`
    -   `zookeeper.session.timeout.ms`
    -   `zookeeper.connection.timeout.ms`
    -   `zookeeper.sync.time.ms`
    -   `offsets.storage`
    -   `offsets.channel.backoff.ms`
    -   `offsets.channel.socket.timeout.ms`
    -   `offsets.commit.max.retries`
    -   `dual.commit.enabled`
    -   `partition.assignment.strategy`
    -   `socket.receive.buffer.bytes`
    -   `fetch.min.bytes`
    **Note:** For more information about other optional configuration items, see Kafka official documentation.

    -   [Kafka09](https://kafka.apache.org/0110/documentation.html#consumerconfigs)
    -   [Kafka010](https://kafka.apache.org/090/documentation.html#newconsumerconfigs)
    -   [Kafka011](https://kafka.apache.org/0102/documentation.html#newconsumerconfigs)

## Mapping between Kafka version names and version numbers {#section_ncs_cqg_cgb .section}

|Kafka version name|Kafka version number|
|------------------|--------------------|
|Kafka08|V0.8.22|
|Kafka09|V0.9.0.1|
|Kafka010|V0.10.2.1|
|Kafka011|V0.11.0.2|

## Examples {#section_gzx_dqg_cgb .section}

```language-sql
create table datahub_input (
id VARCHAR,
nm VARCHAR
) with (
type = 'datahub'
);

create table sink_kafka (
 messageKey VARBINARY,
`message` VARBINARY,
 PRIMARY KEY (messageKey)
) with (
    type = 'kafka010',
    topic = '<yourTopicName>',
    bootstrap.servers = '<yourServerAddress>'
);

INSERT INTO
    sink_kafka
SELECT
   cast(id as VARBINARY) as messageKey,
   cast(nm as VARBINARY) as `message`
FROM
    datahub_input;        
```

