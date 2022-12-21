## Implementation Plan

The next stage after specifying a potential approach for publisher curated addressability is a MVP implementation with relevant vendors (SSPs and DSPs).
In the following we describe an implementation plan for involved parties, creating a MVP.

### Package Ia

* Adherence of (SSP to DSP) "authorized connections" restriction configuration
* No restriction of internal DSP graph usage - to be governed by contractual agreement initally
* but no ID exposure, since ID export per default deactivated
* PCA config not automatically crawled yet

### Package Ib

* Adherence of DSP "seat level" restriction configuration but without "authorized feature" binding

### Package II

* Partially adherence of "authorized feature" config especially in respect of IDs being used in DSP internal graphs or not 
* Cross-publisher domain usage of IDs
* PCA config automatically consumed (via API/File and/or configurable via definite GUI)

### Package III

* Full implementation of "authorized feature" configuration
* therefore configure data / ID export 
* therefore configure external graph usage of IDs

### Package IV (TBD at later stage)

* Data usage configuration (e.g. seller-defined audience signalling usage in value chain)
