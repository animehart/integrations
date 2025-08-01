# DomainTools Real Time Unified Feeds

The DomainTools Real Time Unified Feeds integration allows you to monitor DomainTools Newly Observed Domains. 
The DomainTools NOD Feed provides real-time access to newly registered and observed domains, enabling proactive threat detection and defense. 

With over 300,000 new domains observed daily, the feed empowers security teams to identify and block potentially malicious domains before they can be weaponized. 
Ideal for threat hunting, phishing prevention, and brand protection, the NOD Feed delivers unparalleled visibility into emerging domain activity to stay ahead of evolving threats.

For example, if you wanted to monitor Newly Observed Domains (NOD) feed, you could ingest the DomainTools NOD feed. 
Then you can reference domaintools.nod_feed when using visualizations or alerts.

## Data streams

The DomainTools Real Time Unified Feeds integration collects one type of data streams: logs

Log data streams collected by the DomainTools integration include the Newly Observed Domains (NOD) feed: Apex-level domains (e.g. Example Domain  but not www.example.com) that we observe for the first time, and have not observed previously. 
Populated with our global DNS sensor network.

## Requirements

You need Elasticsearch for storing and searching your data and Kibana for visualizing and managing it. 
You can use our hosted Elasticsearch Service on Elastic Cloud, which is recommended, or self-manage the Elastic Stack on your own hardware.

You will require a license to one or more DomainTools feeds, and API credentials. 
Your required API credentials will vary with your authentication method, detailed below. 

Obtain your API credentials from your group’s API administrator. 
API administrators can manage their API keys at research.domaintools.com, selecting the drop-down account menu and choosing API admin.

## Setup

For step-by-step instructions on how to set up an integration, see the Getting started guide.

### Newly Observed Domains (NOD) Feed 

The `nod_feed` data stream provides events from [DomainTools Newly Observed Domains Feed](https://www.domaintools.com/products/threat-intelligence-feeds/).
This data is collected via the [DomainTools Real Time Feeds API](https://docs.domaintools.com/feeds/realtime/).

#### Example

An example event for `nod_feed` looks as following:

```json
{
    "@timestamp": "2025-06-17T05:55:49.465Z",
    "agent": {
        "ephemeral_id": "342683ed-b707-4537-bf91-16233fc78a31",
        "id": "df6cda61-c87d-40c3-92d1-6eb4f18f3a79",
        "name": "elastic-agent-42619",
        "type": "filebeat",
        "version": "8.15.3"
    },
    "data_stream": {
        "dataset": "ti_domaintools.nod_feed",
        "namespace": "30698",
        "type": "logs"
    },
    "domaintools": {
        "domain": "test1.com",
        "timestamp": "2025-01-11T08:42:46Z"
    },
    "ecs": {
        "version": "8.17.0"
    },
    "elastic_agent": {
        "id": "df6cda61-c87d-40c3-92d1-6eb4f18f3a79",
        "snapshot": false,
        "version": "8.15.3"
    },
    "event": {
        "agent_id_status": "verified",
        "category": [
            "threat"
        ],
        "dataset": "ti_domaintools.nod_feed",
        "ingested": "2025-06-17T05:55:52Z",
        "kind": "enrichment",
        "type": [
            "indicator"
        ]
    },
    "host": {
        "architecture": "x86_64",
        "containerized": true,
        "hostname": "elastic-agent-42619",
        "id": "328e5cd3dfd442488a3dd49bf596f391",
        "ip": [
            "192.168.241.2",
            "192.168.254.4"
        ],
        "mac": [
            "02-42-C0-A8-F1-02",
            "02-42-C0-A8-FE-04"
        ],
        "name": "elastic-agent-42619",
        "os": {
            "codename": "focal",
            "family": "debian",
            "kernel": "3.10.0-1160.119.1.el7.x86_64",
            "name": "Ubuntu",
            "platform": "ubuntu",
            "type": "linux",
            "version": "20.04.6 LTS (Focal Fossa)"
        }
    },
    "input": {
        "type": "cel"
    },
    "message": "{\"timestamp\":\"2025-01-11T08:42:46Z\",\"domain\":\"test1.com\"}",
    "threat": {
        "feed": {
            "description": "Apex-level domains (e.g. example.com but not www.example.com) that we observe for the first time, and have not observed previously with our global DNS sensor network.",
            "name": "DomainTools NOD",
            "reference": "https://docs.techdocs.ci.domaintools.cloud/feeds/realtime/userguide/"
        },
        "indicator": {
            "name": "test1.com",
            "type": "domain-name"
        }
    }
}
```

**Exported fields**

| Field | Description | Type |
|---|---|---|
| @timestamp | Date/time when the event originated. This is the date/time extracted from the event, typically representing when the event was generated by the source. If the event source has no original timestamp, this value is typically populated by the first time the event was received by the pipeline. Required field for all events. | date |
| data_stream.dataset | The field can contain anything that makes sense to signify the source of the data. Examples include `nginx.access`, `prometheus`, `endpoint` etc. For data streams that otherwise fit, but that do not have dataset set we use the value "generic" for the dataset value. `event.dataset` should have the same value as `data_stream.dataset`. Beyond the Elasticsearch data stream naming criteria noted above, the `dataset` value has additional restrictions:   \* Must not contain `-`   \* No longer than 100 characters | constant_keyword |
| data_stream.namespace | A user defined namespace. Namespaces are useful to allow grouping of data. Many users already organize their indices this way, and the data stream naming scheme now provides this best practice as a default. Many users will populate this field with `default`. If no value is used, it falls back to `default`. Beyond the Elasticsearch index naming criteria noted above, `namespace` value has the additional restrictions:   \* Must not contain `-`   \* No longer than 100 characters | constant_keyword |
| data_stream.type | An overarching type for the data stream. Currently allowed values are "logs" and "metrics". We expect to also add "traces" and "synthetics" in the near future. | constant_keyword |
| domaintools.domain | The Domain. Apex-level domains (e.g. example.com but not www.example.com) that we observe for the first time, and have not observed previously with our global DNS sensor network. | keyword |
| domaintools.feed | The feed. | keyword |
| domaintools.timestamp | Timestamp when the domain was added to the DomainTools feed, in ISO 8601 UTC form. | date |
| input.type | Type of filebeat input. | keyword |
| labels.is_ioc_transform_source | Indicates whether an IOC is in the raw source data stream, or the in latest destination index. | constant_keyword |
| message | The feed. | match_only_text |


