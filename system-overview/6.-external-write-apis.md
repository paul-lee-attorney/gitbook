---
icon: up-right-from-square
---

# 6. External Write APIs

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

<details>

<summary>6.3. <strong>APIs Routed to BMM Keeper</strong></summary>

<table><thead><tr><th width="79.625">S.N.</th><th width="299.6953125">API</th><th>Description of Functions and Input Parameters</th></tr></thead><tbody><tr><td>11</td><td><p>function nominateOfficer(</p><p>  uint256 <em><mark style="color:blue;">seqOfPos</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">candidate</mark></em></p><p>) external</p></td><td>(The Director having the nomination right) Nominate the user identified by its user number as <em><mark style="color:blue;">candidate</mark></em> for the officer’s position numbered as <em><mark style="color:blue;">seqOfPos</mark></em>.</td></tr><tr><td>12</td><td><p>function createMotionToRemoveOfficer(</p><p>uint256 <em><mark style="color:blue;">seqOfPos</mark></em></p><p>) external</p></td><td>(The Director having the nomination right) Create a draft Motion to remove the officer on the position numbered as <em><mark style="color:blue;">seqOfPos</mark></em>.</td></tr><tr><td>13</td><td><p>function createMotionToApproveDoc(</p><p>  uint256 <em><mark style="color:blue;">doc</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">seqOfVR</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">executor</mark></em></p><p>) external</p></td><td>(Any Director) Creates a draft Motion for the Board to approve the document deployed at the address of <em><mark style="color:blue;">doc</mark></em>  as per the voting rule numbered as <em><mark style="color:blue;">seqOfVR</mark></em> with the user numbered as <em><mark style="color:blue;">executor</mark></em> to invoke it.</td></tr><tr><td>14</td><td><p>function createAction(</p><p>    uint256 <em><mark style="color:blue;">seqOfVR</mark></em>,</p><p>    address[] memory <em><mark style="color:blue;">targets</mark></em>,</p><p>    uint256[] memory <em><mark style="color:blue;">values</mark></em>,</p><p>    bytes[] memory <em><mark style="color:blue;">params</mark></em>,</p><p>    bytes32 <em><mark style="color:blue;">desHash</mark></em>,</p><p>    uint256 <em><mark style="color:blue;">executor</mark></em></p><p>) external</p></td><td>Create a draft Motion for the Board to invoke a series of calls, as per the voting rule numbered as <em><mark style="color:blue;">seqOfVR</mark></em>, to the contracts deployed at their respective addresses of <em><mark style="color:blue;">targets</mark></em>, with paying ETH amount to <em><mark style="color:blue;">values</mark></em>, and inputting parameters of <em><mark style="color:blue;">params</mark></em>, attached with the hash value of the description message as <em><mark style="color:blue;">desHash</mark></em>, with the user numbered as <em><mark style="color:blue;">executor</mark></em> to invoke it.</td></tr><tr><td>15</td><td><p>function entrustDelegaterForBoardMeeting(</p><p>  uint256 <em><mark style="color:blue;">seqOfMotion</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">delegate</mark></em></p><p>) external</p></td><td>(Any Directors) Entrust the user numbered as <em><mark style="color:blue;">delegate</mark></em> to cast vote in Board meeting for the Motion identified as <em><mark style="color:blue;">seqOfMotion</mark></em>.</td></tr><tr><td>16</td><td><p>function proposeMotionToBoard (</p><p>  uint256 <em><mark style="color:blue;">seqOfMotion</mark></em></p><p>) external</p></td><td>(Any Director) Propose the draft Motion numbered as <em><mark style="color:blue;">seqOfMotion</mark></em> to the Board meeting.</td></tr><tr><td>17</td><td><p>function castVote(</p><p>  uint256 <em><mark style="color:blue;">seqOfMotion</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">attitude</mark></em>,</p><p>  bytes32 <em><mark style="color:blue;">sigHash</mark></em></p><p>) external</p></td><td>(Any Director) Casts vote with the <em><mark style="color:blue;">attitude</mark></em> for the Motion numbered as <em><mark style="color:blue;">seqOfMotion</mark></em> with the signature message’s hash value as <em><mark style="color:blue;">sigHash</mark></em>.</td></tr><tr><td>18</td><td><p>function voteCounting(</p><p>  uint256 <em><mark style="color:blue;">seqOfMotion</mark></em></p><p>) external</p></td><td>(Any user) Count the vote result for the Motion numbered as <em><mark style="color:blue;">seqOfMotion</mark></em>.</td></tr><tr><td>19</td><td><p>function execAction(</p><p>    uint <em><mark style="color:blue;">typeOfAction</mark></em>,</p><p>    address[] memory <em><mark style="color:blue;">targets</mark></em>,</p><p>    uint256[] memory <em><mark style="color:blue;">values</mark></em>,</p><p>    bytes[] memory <em><mark style="color:blue;">params</mark></em>,</p><p>    bytes32 <em><mark style="color:blue;">desHash</mark></em>,</p><p>    uint256 <em><mark style="color:blue;">seqOfMotion</mark></em></p><p>) external</p></td><td>(The designated executor) Executes the Motion numbered as <em><mark style="color:blue;">seqOfMotion</mark></em>, categorized as <em><mark style="color:blue;">typeOfAction</mark></em>, to invoke the series of calls to the contracts deployed at addresses of <em><mark style="color:blue;">targets</mark></em>, with paying the respective ETH amount to <em><mark style="color:blue;">values</mark></em>, inputting parameters as <em><mark style="color:blue;">params</mark></em>, attached with description message’s hash value as <em><mark style="color:blue;">desHash</mark></em>.</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/bmmkeeper-11.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bmmkeeper-12.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bmmkeeper-13.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bmmkeeper-14.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bmmkeeper-15.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bmmkeeper-16.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bmmkeeper-17.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bmmkeeper-18 (1).jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bmmkeeper-19.jpg" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>6.4. <strong>APIs Routed to ROM Keeper</strong></summary>

<table><thead><tr><th width="49.73046875" align="center">S.N.</th><th width="261.87890625">API</th><th>Description of Functions and Input Parameters</th></tr></thead><tbody><tr><td align="center">20</td><td><p>function setMaxQtyOfMembers(</p><p>  uint256 <em><mark style="color:blue;">max</mark></em></p><p>) external</p></td><td>(The sectary of company, i.e. the Direct Keeper of General Keeper) Set the max quantity of Members as <em><mark style="color:blue;">max</mark></em>.</td></tr><tr><td align="center">21</td><td><p>function setPayInAmt(</p><p>  uint256 <em><mark style="color:blue;">seqOfShare</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">amt</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">expireDate</mark></em>,</p><p>  bytes32 <em><mark style="color:blue;">hashLock</mark></em></p><p>) external</p></td><td>(The sectary of company, i.e. the Direct Keeper of General Keeper) Set the intended pay in amount of <em><mark style="color:blue;">amt</mark></em> for the share numbered as <em><mark style="color:blue;">seqOfShare</mark></em>, before the date of <em><mark style="color:blue;">expireDate</mark></em>, with the hash lock whose hash value is <em><mark style="color:blue;">hashLock</mark></em>.</td></tr><tr><td align="center">22</td><td><p>function requestPaidInCapital(</p><p>bytes32 <em><mark style="color:blue;">hashLock</mark></em>,</p><p>string memory <em><mark style="color:blue;">hashKey</mark></em></p><p>) external</p></td><td>(The Member, after paying the paid in the relevant price off-chain) Request the specific paid in amount for the target share by inputting the hash key string <em><mark style="color:blue;">hashKey</mark></em> to unlock the hash lock whose hash value is <em><mark style="color:blue;">hashLock</mark></em>.</td></tr><tr><td align="center">23</td><td><p>function withdrawPayInAmt(</p><p>  bytes32 <em><mark style="color:blue;">hashLock</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">seqOfShare</mark></em></p><p>) external</p></td><td>(The secrtary of the company, i.e. the Direct Keeper of General Keeper, after the expiration date of the relevant hash lock) Withdraw the setting for granting the pay in amount for the specific share numbered as <em><mark style="color:blue;">seqOfShare</mark></em>, by inputting the hash lock value <em><mark style="color:blue;">hashLock</mark></em>.</td></tr><tr><td align="center">24</td><td><p>function payInCapital(</p><p>  uint256 <em><mark style="color:blue;">seqOfShare</mark></em>,</p><p>  uint256 <em><mark style="color:blue;">amt</mark></em></p><p>) external payable</p></td><td>(The shareholder) Pay in capital for the share numbered as <em><mark style="color:blue;">seqOfShare</mark></em> to gain the paid-in amount of <em><mark style="color:blue;">amt</mark></em>  by paying ETH with the equivalent value to the General Keeper.</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/romkeeper-20 (1).jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/romkeeper-21.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/romkeeper-22.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/romkeeper-23.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/romkeeper-24.jpg" alt=""><figcaption></figcaption></figure>

</details>

