---
icon: up-right-from-square
---

# External Write APIs

There are totally 【91】 external write APIs exposed by the system, which collectively encompass nearly all legal acts relating to corporate governance, share transactions, and the payment and receipt of ETH and/or USDC. These APIs are routed to various Sub-Keepers for further processing and execution, thereby effectuating the corresponding legal consequences of each act.

<details>

<summary>6.1.  APIs routed to ROC Keeper</summary>

<table><thead><tr><th width="83.83203125">S.N.</th><th width="198.00390625">API</th><th>Description of Functions and Input Parameters</th></tr></thead><tbody><tr><td>01</td><td>function createSHA(<br>  uint <em><mark style="color:blue;">version</mark></em><br>) external</td><td>(Any Member) Create a new shareholders agreement by cloning the Template of the specific <em><mark style="color:blue;">version</mark></em>.</td></tr><tr><td>02</td><td><p>Function circulateSHA(</p><p>  address <em><mark style="color:blue;">body</mark></em>,</p><p>  bytes32 <em><mark style="color:blue;">docUrl</mark></em>,</p><p>  bytes32 <em><mark style="color:blue;">docHash</mark></em></p><p>) external</p></td><td>(The Owner of the draft) Circulate the finalized draft of shareholders agreement deployed at the address of <em><mark style="color:blue;">body</mark></em> to the contractual parties for signing, with the URL infomation of <em><mark style="color:blue;">docUrl</mark></em>, and hash value of <em><mark style="color:blue;">docHash</mark></em>.</td></tr><tr><td>03</td><td><p>function signSHA(</p><p>  address <em><mark style="color:blue;">sha</mark></em>,</p><p>  bytes32 <em><mark style="color:blue;">sigHash</mark></em></p><p>) external</p></td><td>(Parties to the draft) Sign the finalized draft of shareholders agreement deployed at the address of <em><mark style="color:blue;">sha</mark></em>, with the hash value of signature as <em><mark style="color:blue;">sigHash</mark></em>.</td></tr><tr><td>04</td><td><p>function activateSHA(</p><p>  address <em><mark style="color:blue;">body</mark></em></p><p>) external</p></td><td>(Any user) Activate the draft of shareholders agreement deployed at the address of <em><mark style="color:blue;">body</mark></em>.</td></tr><tr><td>05</td><td><p>function acceptSHA(</p><p>  bytes32 <em><mark style="color:blue;">sigHash</mark></em></p><p>) external</p></td><td>(Any user) Accept the terms and conditons of SHA in force, with the hash value as <em><mark style="color:blue;">sigHash</mark></em>.</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/rockeeper-01.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/rockeeper-02.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/rockeeper-03 (1).jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/rockeeper-04.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/rockeeper-05 (1).jpg" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>6.2. <strong>APIs Routed to ROD Keeper</strong></summary>



<table><thead><tr><th width="78.9296875">S.N.</th><th width="229.31640625">API</th><th>Description of Functions and Input Parameters</th><th></th></tr></thead><tbody><tr><td>06</td><td><p>function takeSeat(</p><p>  uint256 <em><mark style="color:blue;">seqOfMotion</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">seqOfPos</mark></em></p><p>) external</p></td><td>(The elected Director) Assume the director’s seat identified by <em><mark style="color:blue;">seqOfPos</mark></em> pursuant to the authorization granted under the Motion identified by <em><mark style="color:blue;">seqOfMotion</mark></em>.</td><td></td></tr><tr><td>07</td><td><p>function removeDirector (</p><p>  uint256 <em><mark style="color:blue;">seqOfMotion</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">seqOfPos</mark></em></p><p>) external</p></td><td>(The Member having the nomination right) Remove the director on the position numbered as <em><mark style="color:blue;">seqOfPos</mark></em> as per the removal Motion numbered as <em><mark style="color:blue;">seqOfMotion</mark></em>.</td><td></td></tr><tr><td>08</td><td><p>function takePosition(</p><p>  uint256 <em><mark style="color:blue;">seqOfMotion</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">seqOfPos</mark></em></p><p>) external</p></td><td>(The elected officer) Take the officer position identified as <em><mark style="color:blue;">seqOfPos</mark></em> pursuant to the authorization granted under the Motion identified as <em><mark style="color:blue;">seqOfMotion</mark></em>.</td><td></td></tr><tr><td>09</td><td><p>function removeOfficer (</p><p>  uint256 <em><mark style="color:blue;">seqOfMotion</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">seqOfPos</mark></em></p><p>) external</p></td><td>(The executor) Remove the executive officer on the position numbered as <em><mark style="color:blue;">seqOfPos</mark></em> as per the removal Motion numbered as <em><mark style="color:blue;">seqOfMotion</mark></em>.</td><td></td></tr><tr><td>10</td><td><p>function quitPosition(</p><p>  uint256 <em><mark style="color:blue;">seqOfPos</mark></em></p><p>) external</p></td><td>(The Director or officer) Quit the position identified as <em><mark style="color:blue;">seqOfPos</mark></em> voluntarily.</td><td></td></tr></tbody></table>

<figure><img src="../.gitbook/assets/rodkeeper-06 (1).jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/rodkeeper-07.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/rodkeeper-08.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/rodkeeper-09.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/rodkeeper-10 (5).jpg" alt=""><figcaption></figcaption></figure>

</details>

