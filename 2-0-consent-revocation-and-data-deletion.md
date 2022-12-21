## Consent Revocation and Data Deletion

Following the above approach, dealing with consent revocation and data deletion requests becomes tangible for 1st parties given they are, even in a minimal viable setup, in control where data is being transmitted (configuration) and for which functionality is used (configuration and contractual agreement).

Based on this it is clear which parties need to react to deletion requests and also a differentiation w.r.t. functionality and scope, furthermore does the contractual agreement allow to define how deletions should take place.  

In general there are three topics to take into consideration

1. Stopping data processing
2. Deletion of data - IDs themselves and associated data
3. Scope of deletion

### Deletion w.r.t. bidding/ad-server (Client Side availability)

In terms of processing on the client side w.r.t. ro the respective functions, data / IDs are only transmitted / processed in the presence of user consent. This is the publisher/advertisers responsibility, details depend on their respective setup. AdServer/ SSP act as processors and will rely on the service owner to only provide consented data.

This should generally mean that:

1. IDs are purged from an End-Users Device - **Note that** given client side matching is disabled and processing is ideally done server to server, IDs should only be present on 1st party domains and native apps controlled by the respective publisher and thus deletion is possible.

    W.r.t to the above the on-device storage mechanism for IDs is irrelevant, whether an ID is stored in a Cookie or a native storage mechanism of a mobile device does not matter in this context. IDs themselves might be derived from CRM/Server-Side Information (Authenticated Users etc.)

2. Provisioning of IDs as described above is terminated, thus processing stops effectively from a users perspective

Notwithstanding the above, depending on the detailed agreement parties in such a setup can assume joint-controller roles, but do so on the configured and contractually agreed basis.

### Server-Side deletion of data

While stopping the processing seems the most urgent topic in the context of a revocation, 1st parties will also need defined APIs to ensure proper deletion processes take place. In general one could think of implementing this in two ways:

#### Real-Time deletion - within/parallel to bidding initiated from the client

While this seems interesting in terms of time to completion, this would require the transmission of a not-consented ID/retaining it for the purposes of deletion on the client. This seems difficult to structure and is contrary to the goal to immediately stop client side processing (which is the likely most impactful direct change from a users perspective)

#### Bidding independent deletion

In order to process deletions with the known platforms/parties it is required for the publisher/advertiser to provide the respective IDs to be deleted.  Technically both real-time as well as push/pull models with batches are generally thinkable. In the sense of a process which is focussed on robustness rather than speed, batch based models seem to be best fit for purpose.

Technically this could be a push or a pull (to/from known platforms/parties), it seems most tangible to use mechanisms which are already in place for audience segment uploads etc.

#### Scope of deletion

In general deletion can mean two things - either the deletion of the ID provided in the deletion request (thus detaching the data from being used (and likely making it anonymous/useless) or deletion of **_all records_** associated with the IDs. Which one applies will depend on the detailed legal setup of how publishers/advertisers collected the respective data and the framing.

**Remark** - We refer to deletion here as it relates to storage of IDs and associated data in terms of systems/usage to implement/execute a function within digital marketing. That means a CRM (which retains data for the purposes of consuming a specific service) is different from a DMP (which retains data for purposes of digital marketing).

One might need to delete data in a DMP given the user revoked a consent to use a profile (age for example) as a segment in a campaign, but this does not automatically entail the need to delete the very same information from a CRM system. Details are subject to legal grounds for processing and retention of data.

A challenge is the notion of combined/global profiles. The goal should be to avoid by default the merging of segment information into combined user profiles (given its hard to disentable that later) as it almost automatically results in a joint controller setup and issues to deal with requests for information by end-users. Ideally audience information is kept in separate partitioned silos and only dynamically matched as needed (and allowed for based on configuration and contractual agreement). Clean Rooms and new privacy enhancing technologies (PET) can be implemented for more stringent implementations (technical guarantees), but simply avoiding this in a classical setup will be a high benefit by itself.

This also addresses concerns around “Zombie Profiles” where a profile is actually never deleted and as soon as a user re-consents his full (maybe month old) profile is resurrected.

Other than that there might need to be additional considerations based on how publishers and buy side platforms agreed with respect to the use for certain functionality.

* Deletion of Audience Segment
* Use within Capping, Campaign Control Counters
* ….
