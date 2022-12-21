## General considerations

To enable publisher to control if, how, when and by whom data is processed the following means can be applied:

1. configurational/technical control
2. contractual control

The general assumption is to **favor technical control/signaling** over mere contractual agreements given the former is both more scalable and can largely simplify additional contractual agreements as they are needed.

**Having said that**, both will play a key role given there is no realistic / scalable means outlook as of now how publishers could end-to-end enforce - once data has been provided - a signal for one function (frequency control on a buy side platform) vs another (audience building for a specific buy side seat).

As of now there are no ideas on the table how to enable a completely open market with any number of buy side platforms - following ideas always rely on a contractual binding between publisher/sales house and demand side platform, besides the existing contractual relations.

**Also note** that data encryption approaches for id signals are not analyzed in depth here, given encryption solutions largely focus on preventing leaks of data in transit. This by itself does not address large portions of the described problem statement and comes with an additional set of challenges on governance etc. al.

Specifically the following topics are not easily addressed solely relying on encryption

* **Recipient of signals / data**- controlling access to information solely based on a third party (from a pubs perspective) governance system (which manages access to decryption) does not seem sufficient, or at least highly dependent on the exact implementation of this governance system. Encryption based approach typically assume a broadcast scenario that is controlled via access to decryption keys.
* **Legal questions** - Assuming the governance system would largely control the access to data by service providers, this might lead to legal considerations w.r.t. joint controllership between the operator of the governance system and the individual first parties leveraging that system
* **Functional Control / Business Considerations** - Encryption can hardly serve both as a data leakage / security mechanism **AND** a mechanism which allows first parties to determine by whom/for what their data may be used by which parties.

Encryption is also a key component in various proposals that rely on browser/platforms and their interactions with specifically designed computing environments that offer privacy/data leakage (lack thereof) guarantees. These systems rely on homomorphic encryption (i.e. functions/results are calculated on encrypted data) and multi-party computation (to avoid the need for a single trusted environment) and are dubbed as **privacy enhancing technologies**.

Those might be able to address the above mentioned shortcoming, but are currently just proposals which will take substantial multi-stakeholder commitments and implementation effort. Once available they might provide the ability to shift even more concerns out of contractual control towards technical control.

&gt;&gt; [General Approach](1-1-general-approach.md)