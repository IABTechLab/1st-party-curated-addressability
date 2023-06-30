## Authorized Connections/Functions

**Open Items**

* Publisher Config Source for SSP (URL/Admin Tool) per Domain/per Sales House
* Publisher Config Source for DSP - fetched using crawler (URL via pub/sales house), secured or not (.htaccess….)
* Eviction Policy (Daily, ….) via config, vs. fixed default -> See Config Mechanisms id-sources.json
* Additional SSP -> DSP Config vs. Handling via PreBid
* Contract Ref - Take or Leave
* ID-Sources JSON relevance

**Remarks**

* Real-Time signaling of functions out of scope for now
* Some features might be configurable or not initially
* Features initially strings, later maybe standardized
* Config object describes usage, transmission of IDs configured with SSP
* To avoid complexity explosion no per ID/function config

In order to reach the desired goals, this proposal introduces two new conceptual approaches to define trusted data processing flows.

1. **Authorized Connections** - allowing a publisher to define trusted connections from its properties, to SSPs and DSPs
2. **Authorized Functions** - allowing a publisher to define permissible functionality / use of its data

 Note that in scenarios that involve clean-rooms, authorized connections might not be needed (in case no IDs are transmitted in the bid-stream at all) or setup differently.

### Authorized Connections

Authorized Connections are defined in two stages. The first one that defines which IDs/data may be passed to bidders (SSPs) is already available in [PreBid](https://docs.prebid.org/dev-docs/modules/userId.html#permissions), the second one that defines the permissible calls/connections to DSPs is new.

#### 1. Publisher to SSP configuration

Publishers can control which user ids are shared with the bid adapters they choose to work with by using the bidders array. The bidders array is part of the User id module config, publisher may choose to send an id to some bidders but not all, the default behavior is that each user id go to all bid adapters the publisher is working with.
Use the optional bidders parameter to define an array of bidder codes to which this user ID may be sent.
In this example the SharedID sub adapter is only allowed to be sent to the XandR and Yieldlab adapter.

In reference to step 1 in the [General Approach](https://github.com/avuim/publisher-curated-auctioning/blob/main/1-1-general-approach.md#general-approach) - this allows the publisher to control the information flow to its trusted SSPs of choice.

```json
{
 "userIds": [{
  "name": "sharedId",
  "bidders": [
   "xandr", "yieldlab"
  ]
 }]
}
```

#### 2. SSP to DSP configuration

In order to define the allowed connections/calls to be made to demand platforms in reference to step 2 in the [General Approach](https://github.com/avuim/publisher-curated-auctioning/blob/main/1-1-general-approach.md#general-approach) - The following configuration object will allow the publisher to control the information flow from its trusted SSPs (defined in step 1) to its trusted DSPs of choice.

Note: ID specific configuration is a highly critical topic since it quickly creates high bid request costs (bid duplication). Therefore this configuration (at least initially) includes an "appliesToId" parameter which defines, extending PreBid configuration, for which identifiers this configuration on SSP side should apply to.

If it is not set, the configuration automatically applies to all UserIDs listed in the PreBid UserID configuration, effectively defining the DSP to which the SSP may send request overall. In case its configured it allows the publisher to define the allowed connections/calls for the given specific sub-set of ids which need special treatment/protection (i.e. only those DSP to which the publisher has a direct contractual relation).

Furthermore, no seatid specific configurations are currently realistic, locking at the cost of implementation.

```json
{
 "sspConfig": [{
  "version": "0.0.1",
  "updatedAt": "{TIMESTAMP}",
  "appliesToId": ["netId","rampId"],
  "authorizedConnections": [{
    "xandr": ["DSP_1", "DSP_2", "DSP_n"]
   },
   {
    "yieldlab": ["DSP_1", "DSP_2", "DSP_n"]
   }
  ]
 }]
}
```

##### Object: sspConfig

The sspConfig object is the top-level of the ssp config JSON file. It defines the version, last update date of the config file as well as it core the SSP object further defining the DSPs to which they should handover IDs signalled by e.g. Prebid userId module.

| Attribute | Type | Description
| -------------- | ----------- |-------------- |
| version | string; required | The version of this config file |
| upatedAt | timestamp; required | When was config file updated |
| appliesToId | array of strings; optional | defines to which IDs the SSP configuration applies. In case it is not specified, the configuration should apply to all ids in the the bid request |
| authorizedConnections | object; required | DSP ID signaling whitelist configuration per SSP |

##### (Sub-)Object: authorizedConnections

| Attribute | Type | Description
| -------------- | ----------- |-------------- |
| {ssp} | string; required | name/id of SSP as defined in doc |
| {dsps} | array of strings; required | name/id of DSP as defined in doc  |

### Authorized Functions (DSP Config)

```json
{
 "dspConfig": [{
  "version": "0.0.1",
  "updatedAt": "{TIMESTAMP}",
  "dsp": [
   {
    "adform": [{
      "seatId": [0],
      "authorizedFunctions": ["{function_1}", "{function_2}", "{function_n}"],
      "contractReference": "{contract}"
     },
     {
      "seatId": ["foo"],
      "authorizedFunctions": ["{function_1}", "{function_2}", "{function_n}"],
      "contractReference": "{contract}"
     },
     {
      "seatId": ["foo123", "foo456", "foo789"],
      "authorizedFunctions": ["{function_1}", "{function_2}", "{function_n}"],
      "contractReference": "{contract}"
     }
    ]
   },
   {
    "activeagent": [{
     "seatid": [0],
     "authorizedFunctions": ["{function_1}", "{function_2}", "{function_n}"],
     "contractReference": "{contract}"
    }]
   }
  ]
 }]
}
```

#### Object: dspConfig

| Attribut | Type | Description
| -------------- | ----------- |-------------- |
| version | string; required | The version of this config file |
| upatedAt | timestamp; required | When was config file updated |
| dsp | object; required | Object of dsp specific configs |

#### (Sub-)Object: dsp

| Attribut | Type | Description
| -------------- | ----------- |-------------- |
| {dsp} | object; required | seat ID (-range/-list) specific configuration of functions allowed |
| seatId | array of strings; required | In case [0] alls seats are whitelisted, alternatively a single ID ["foo"] or an array of seats ["foo_1","foo_n"] can be listed |
| authorizedFunctions | array of strings; required |  |
| contractReference | string; optional | reference to contract |

**Notes:**

1. This configuration is private by default (deny) this is an allow list mechanism
2. Function config is specific, single seat config prevails over wildcards (subsidiarity principle)

### Metadata

#### ID Provider Table

| Name | Comment
| -------------- | ----------- |
| netId | | |
| rampId | | |
| sharedId | | |
| uid2 | | |
| idplus | | |

#### Feature Table

| Name | Comment
| -------------- | ----------- |
| bidding | | |
| fc | | |
| forecasting | | |
| attribution | | |
| optimization | | |
| loglevel-export | | |

#### DSP Table

| Name | Status | Reference | Comment
| -------------- | ----------- |-------------- | ----------- |
| AdForm | Active | | |
| ActiveAgent | Active | | |
| Xandr | Active | a.k.a. AppNexus | |
| Adthink| Active | | |
| Amobee | Active | | |
| Criteo | Active | | |
| DiscoverTech | Active | | |
| DV360 | Active | | |
| Hivestack | Active | | |
| MediaMath | Active | | |
| Mediarithmics | Active | | |
| Platform161 | Active | | |
| RTBHouse | Active | | |
| AmazonDSP | Deprecated | a.k.a. Sizmek |  |
| SmartyAds | Active | | |
| Splicky | Active | | |
| Teads | Active | | |
| TheTradeDesk | Active | | |
| Yahoo| Active | | former Verizon Media|

#### SSP Table

| Name | Status | Reference | Comment
| -------------- | ----------- |-------------- | ----------- |
| AdForm | Active | | |
| Adswizz | Active | | |
| Azerion | Active | a.k.a Improve Digital | |
| Bidswitch | Active | | |
| Broadsign | Active | | |
| EMXDigital | Active | | |
| Freewheel | Active | | |
| GoogleAdManager | Active | | |
| Hivestack | Active | | |
| IndexExchange | Active | | |
| OpenX | Active | | |
| Pubmatic | Active | | |
| Magnite | Active | | |
| Smaato | Active | | |
| Equativ | Active | a.k.a. SmartAdserver | |
| Smartclip | Active | | |
| SmartstreamTV | Active | | |
| SpotX | Active | | |
| Stroer | Active | | |
| SSP1 | Active | | |
| Teads | Active | | |
| Triplelift | Active | | |
| VIOOH  | Active | | |
| Yieldlab | Active | | |
| YOCVISX | Active | | |
| Unruly | Active | | |
| YahooExchange | Active | | |
| Xandr | Active | | |

&gt;&gt; [Consent Revocation and Data Deletion](2-0-consent-revocation-and-data-deletion.md)
