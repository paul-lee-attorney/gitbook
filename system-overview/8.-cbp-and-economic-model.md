# 💰 8. CBP and Economic Model

To measure and collect license fees for authors, the system introduced an ERC-20 token "**ComBoox Points**" ("**CBP**").

<details>

<summary><strong>The Attributes and Specifications of CBP</strong></summary>

* Name: ComBooxPoints
* Symbol: CBP
* Standard: ERC20
* Book-Entry Contract:  [**RegCenter**](https://app.gitbook.com/s/bTRjM2PujnZxSvv5X3VP/source-code/regcenter)
* Unit: CBP
* Minimum unit: Lee
* Conversion formula: 1 CBP = 10^18 Lee

</details>

{% hint style="info" %}
**CBP** does **NOT** represent any equity share or ownership share of any entities, and does **NOT** have any beneficiary interests of equity or trust, which is only aimed to collect license fees for smart contracts in **ComBoox**.  The value of **CBP** may fluctuate from time to time depending on the number of users and registered companies in **ComBoox**, which may reflect the value change of the smart contracts concerned with respect to their intellectual property rights.
{% endhint %}

In order to reduce **the uncertainty of CBP prices**, especially to avoid the risk of "**price increase**" brought about by the increase in user stickiness, we deliberately adopt a basic pricing model of "**Fixed Maximum Price, Adjustable Promotion Policy**”.

**ComBoox's economic model** and **license fee** can be summarized as follows:

<details>

<summary>8.1<strong>. Rate of Royalty</strong></summary>

The **author** may set the rate of royalty for any write APIs of the **contract templates**. Each time a user calls the said API to exercise rights, a calculated license fee will be transferred from its account to the **author’s account**. Once set, the rate will be fixed on the particular **contract template**, based on which, **clone contracts** will inherit the same **rate of royalty**.

</details>

<details>

<summary>8.2. <strong>Collection of License Fee</strong></summary>

When a **user** exercise rights by calling a contract's chargeable API, the contract will automatically call **RegCenter** to query the caller’s user number. Thereafter, the **Register** will charge a specific amount of **CBP** from the caller's **Prime Key** account based on the rate of royalty set in the template, and pay to the **author**.

</details>

<details>

<summary>8.3. <strong>Commission of Platform</strong></summary>

For each license fee payment, **ComBoox** charges a commission of up to 20%, which is directly transferred to the **Owner** of **ComBoox**. From time to time, **ComBoox** may revise its promotional policies to reduce the commission rate or establish a minimum royalty rate to ensure coverage of its operational costs. As such, while the platform’s maximum commission rate is fixed at 20%, the actual amount payable may vary based on applicable discount policies.

</details>

<details>

<summary>8.4. <strong>Promotion Policy</strong></summary>

**Author** may create or adjust its license fee at any time by providing users a certain amount of **coupon** or a certain rate of **quantity discount**. Therefore, the original royalty rate set by author when deploying template actually is the ceiling rate.&#x20;

License Fee Payable = Royalty Rate - Total Coupon - Number of Calls ∗ Quantity Discount Rate

</details>

<details>

<summary>8.5. <strong>New User's Gift</strong></summary>

**ComBoox** may introduce promotion policy to give a certain amount of CBP as gift to newly registered **external accounts** from time to time. For details of promotion policy, users can call "Get Platform Rule" API of **Reg Center** to check details.

</details>

<details>

<summary>8.6. <strong>Transfer of Smart Contracts' Copyright</strong></summary>

Smart contracts’ **Author** can freely transfer the templates' copyright to other users. After transfer, license fee for these smart contracts will be paid to **prime key** address of the transferee. The transferee will then be entitled to further transfer the copyright to other users.

</details>

<details>

<summary>8.7. <strong>Transfer of System's Ownership</strong></summary>

**ComBoox’s Owner** can also transfer its ownership to other accounts, thereby transferring the creditor’s right to receivables of platform commission.

</details>



### Source Codes

#### [RegCenter](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/center/RegCenter.sol)
