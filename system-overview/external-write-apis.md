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



