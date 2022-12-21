### Functionality

Open Item - Finalisieren

<table>
  <tr>
   <td colspan="2" >FUNCTIONALITY
   </td>
   <td>Configurable
   </td>
   <td>Per ID
   </td>
   <td>USE CASE
   </td>
   <td>RESTRICTION (FROM SELL TO BUY SIDE)
   </td>
   <td>RESTRICTION (ON BUY SIDE)
   </td>
  </tr>
  <tr>
   <td rowspan="4" >Buying & Optimization
   </td>
   <td>ID based Targeting
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>General processing of a given publisher identifier coming via bid-stream
   </td>
   <td><strong>Minimal Viable Setup </strong>
<p>
Configuration based control which ID/data may be transferred from Pub/Sales House -> SSP/Adserver -> specific DSP.
   </td>
   <td>Restrict seats to be able to bid/not bid on base of an selected ID (ideally,does not seem mandatory in case of controls of other functions).
<p>
DSP enforces permissible use of ID/data as per contractual alignment with Pub/Sales House and/or based on configuration
   </td>
  </tr>
  <tr>
   <td>Frequency Capping
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Capping of user within a specific publisher ID space
   </td>
   <td>Potential technical security mechanism
<ol>

<li>Hashed Anycast: separate ID spaces for broad function categories (Capping/Forecasting vs. Bidding/Targeting) on the publisher side - Hashing capabilities on Pub side (provided by vendor) - no cross pub usage possible in this case

<li>Unhashed Multicast: structured configuration and control on seat level (bid request and functions per seat) without hashing (mulitcast config driven)
</li>
</ol>
   </td>
   <td>Functional Use as per potential future configuration / contractual agreement (with /without seat level settings)
   </td>
  </tr>
  <tr>
   <td>Forecasting
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Impression / ID forecast based on publisher ID space
   </td>
   <td>No restriction if ID is being transferred to DSP - Hashed Anycast, Unhashed Multicast
   </td>
   <td>Functional Use as per potential future configuration / contractual agreement (with /without seat level settingsl)
   </td>
  </tr>
  <tr>
   <td>Algorithmic Optimization
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Using ID to predict value user has for specific campaign
   </td>
   <td>No restriction if ID is being transferred to DSP- Hashed Anycast, Unhashed Multicast
   </td>
   <td>Functional Use as per potential future configuration / contractual agreement (with /without seat level settingsl)
   </td>
  </tr>
  <tr>
   <td rowspan="3" >Reporting
   </td>
   <td>Aggregated Metrics (Uniqueness/Frequency)
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Standard Reporting that aggregates based on ID
   </td>
   <td>No restriction if ID is being transferred to DSP - Hashed Anycast, Unhashed Multicast
   </td>
   <td>Functional Use as per potential future configuration / contractual agreement (with /without seat level settingsl)
   </td>
  </tr>
  <tr>
   <td>Attribution
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Attribution using similar ID space on advertiser and publisher side
   </td>
   <td>Works if ID on Publisher and Advertiser is compatible, and ID send via SSP is similar to ID populated on Advertiser site, must be agreed between publisher/id vendor and advertiser - Unhashed Multicast
   </td>
   <td>ID has to be made available to DSP/Adserver responsible for tracking and compatible with Publisher ID
   </td>
  </tr>
  <tr>
   <td>ID in Log Level Data
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>ID is visible in log-level data exports of a specific vendor
   </td>
   <td>General restriction/encryption of ID, decryption has to be agreed with publisher
   </td>
   <td>General restriction/encryption of ID, decryption has to be agreed with publisher
<p>
Requires agreement/setup with DSP Buy/Side  
   </td>
  </tr>
  <tr>
   <td rowspan="4" >Audience Management
   </td>
   <td>Upload IDs
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Upload IDs into an DMP/DSP Audience
   </td>
   <td>-
   </td>
   <td>No restriction if ID is being transferred to DSP, adopt encryption if needed
   </td>
  </tr>
  <tr>
   <td>Export IDs
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Export IDs to external Platforms (from DMP)
   </td>
   <td> -
   </td>
   <td> Can only be exported in encrypted way, for decryption Publisher needs to involved
   </td>
  </tr>
  <tr>
   <td>Clean Room
   </td>
   <td>
   </td>
   <td>
   </td>
   <td> Ingest Audience from Clean-Room Solution
   </td>
   <td>-
   </td>
   <td>Similar to Upload, as output of Clean-Room overlay is send to DMP in encrypted way
   </td>
  </tr>
  <tr>
   <td>SSP: Combine Deal & Audience
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>Establish pretargeted deal based on 1st Party ID Audience
   </td>
   <td> Only deal id is shared with buyer, ID is visible if shared in bid, all above options are available, alternative is to not share ID but still deal with audience
   </td>
   <td> Only Deal is visible, no restriction needed other than deal itself
   </td>
  </tr>
</table>

&gt;&gt; [Functional Control Format](1-3-functional-control-format.md)
