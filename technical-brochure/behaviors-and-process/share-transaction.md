# 🤝 Share Transaction

The action flow by various stakeholders to promote share transactions through legal behaviors is shown in the table below:

<figure><img src="../../.gitbook/assets/(En)EquityShareTransaction-General.jpg" alt=""><figcaption></figcaption></figure>

The detailed flow of algorithmic instruction interactions between system smart contracts at each step of the action is as follows:

<details>

<summary>(0) Query the caller's user number</summary>

* As the pre-defined process for identity verification, almost each **legal behavior** in the system starts with querying caller's user number.
* **Logical flow**: as follow.

<img src="../../.gitbook/assets/（En）00-msgSender() (1).jpg" alt="" data-size="original">

</details>

### A. Draft Investment Agreement

<details>

<summary>(1)  <strong>Create Investment Agreement</strong></summary>

* **Actor**: it is generally triggered by the share transferor (in share transaction) or the actual controller (in a capital increase transaction)
* **Calling API**: (to be added)
* **Action Consequences**:

1. Create and deploy a new clone contract based on the **investment agreement** contract template;
2. Initialize access control settings for the new **investment agreement** contract;
3. Registering the address of the new **investment agreement** contract in the **investment agreement** registry.

* **Logical flow**: as follows.

<img src="../../.gitbook/assets/（En）01-createIA (1).jpg" alt="" data-size="original">

</details>

<details>

<summary>(2) Appoint General Counsel</summary>

* **Actor**: the creator of **investment agreement**s
* **Calling API**: (to be added)
* **Action Consequences**: Set the **general counsel** role in **investment agreement** to a specific account address;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/02-appointGC.jpg" alt="" data-size="original">

</details>

<details>

<summary>(3) Draft the Contract</summary>

* **Actor:** the **general counsel** of **investment agreement**s
* **Calling API:** (to be added)
* **Action Consequences:** Set the order objects in **investment agreement**;
* **Logical flow:** as follows.

<img src="../../.gitbook/assets/(En)03-addDeal.jpg" alt="" data-size="original">

</details>

<details>

<summary>(4) Set the Signature and Closing Deadline</summary>

* **Actor**: the **general counsel** of **investment agreements**
* **Calling API**: (to be added)
* **Action Consequences**: Set the signature and delivery deadline in **investment agreement**;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/(En)04-setTiming.jpg" alt="" data-size="original">

</details>

<details>

<summary>(5) Set the Parties</summary>

* **Actor:** the **general counsel** of **investment agreement**s
* **Calling API**: (to be added)
* **Action Consequences**: Add or delete a signature for the parties to the contract on the **SigPage** of the **investment agreement**;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/(En)05-addBlank.jpg" alt="" data-size="original">

<img src="../../.gitbook/assets/(En)05-1-removeBlank.jpg" alt="" data-size="original">

</details>

<details>

<summary>(6) Finalize the Contract</summary>

* **Actor:** need to be triggered by the shareholder who creates the contract after reviewing the content;
* **Calling API**: (to be added)
* **Action Consequences:** Revoke the "**Attorney**" in contracts and transfer of the "**Owner**" to a zero address, revoking the right to modify the contract;
* **Logical flow:** as follows.

<img src="../../.gitbook/assets/（EN）06-finalizeIA.jpg" alt="" data-size="original">

</details>

### B. Sign Investment Agreement

<details>

<summary>(7) Circulate the Contract</summary>

* **Actor:** triggered by the **contractual parties**
* **Calling API**: (to be added)
* **Action Consequences:** Write the period of enforcement into the data objects of **investment agreement**s, in accordance with the voting rules in the **investment agreement**;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/（En）07-circualteIA.jpg" alt="" data-size="original">

</details>

<details>

<summary>(8) <strong>Sign the Investment Agreement</strong></summary>

* **Actor:** triggered by the **contractual parties**
* **Calling API**: (to be added)
* **Action Consequences:** Lock the transactions related to the **investment agreement** and record the caller's signature on the first signature page;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/(En)08-signIA.jpg" alt="" data-size="original">

</details>

### C. **Review and Vote for Investment Agreement**

<details>

<summary>(9) Submit to General Meeting</summary>

* **Actor:** triggered by an account that process both **signature** and **shareholder** identity;
* **Calling API**: (to be added)
* **Action Consequences:** Lock the transactions related to the **investment agreement** and record the caller's signature on the first signature page;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/(EN)09-proposeDocOfGM.jpg" alt="" data-size="original">

</details>

<details>

<summary>(10) Delegate </summary>

* **Actor**: triggered by the **shareholders** who have never given delegate;
* **Input parameters:** motion number, the user number of the designated user;
* **Action Consequences**: Vest the number of shareholders giving delegate and the weight of their votes to the designated user;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/（EN）10-entrustDelegateForGM.jpg" alt="" data-size="original">



</details>

<details>

<summary>(11) Vote</summary>

* **Actor**: triggered by the **shareholders** who have never voted or delegated to vote;
* **Input parameters**: motion number, voting attitude, Signature File Hash(selectable);
* **Action Consequences:** Add the votes to ballots case;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/(En)11-castVoteInGM.jpg" alt="" data-size="original">

</details>

<details>

<summary>(12) Ballots</summary>

* **Actor**: triggered any accounts (to avoid the delayed voting calculation by the losing party);
* **Input parameters**: motion number;
* **Action Consequences:** Vest the number of shareholders giving delegate and the weight of their votes to the designated user;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/(En)12-voteCountingOfGM.jpg" alt="" data-size="original">

</details>

### D. Execution of Investment Agreement

<details>

<summary>(13) Deliver the Shares directly</summary>

* **Actor**: The **seller** in the share transfer transaction;
* **Input parameters**: the contract address of **investment agreement** and the deal number;
* **Action Consequences:** **Cancel** the underlying shares of deals and issue new shares with the same class, amount and weight to the **buye**r;
* **Logical flow**: as follows.

<img src="../../.gitbook/assets/(En)13-transferTargetShare (1).jpg" alt="" data-size="original">

</details>







