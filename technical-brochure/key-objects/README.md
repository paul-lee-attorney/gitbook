# 🌻 Key Objects

The **data objects** booked on ComBoox are the "**objects**" of "object oriented programming" the whole system, and in the abstract, they represent different behavioral "subjects", behavioral "objects" or descriptive "objects". in ComBoox system, they either represent economic equity such as **share** and **pledge**, or the equity subjects, behaviors subject such as **shareholders**, **officers** , or the bookkeeping objects such as **rules, motions, resolutions,** etc. The relationships among them reflect various kinds of legal relationships and the legal behaviors logic.

## 1. Share Transactions and General Corporate Governance

The so-called "\*\*Share transaction" refers to the issuance of new shares and transfer of shares in accordance with **investment agreements** such as the Equity Subscription Agreement and the Equity Transfer Agreement. This is the most common and widespread form of corporate share transaction and share bookkeeping is also the basic for the exercise of shareholders' rights.&#x20;

During the operation of the company, all corporate governance behaviors shall take the share registration as basis to verify the identity of shareholders and calculate the voting weights. Whether it is reviewing of share transactions, nomination and executives election, representing the company to sign the smart contracts, pay for tokens and other property, the general governance behaviors of the company is actually reflected in the **motion** **creation**, **proposal** and **voting** process, and all of these behaviors shall take articles of association, **shareholders agreements** and other constitutional documents as basis, in order to determine the specific procedures and conditions to be met. In the system, the shareholders' agreement is a smart contract that summarizes all the **processes, rules and conditions** that need to be followed in corporate governance. Of course, its own changes, as an important corporate governance behavior, should also be regulated and adjusted by its own rules.&#x20;

Therefore, the above share transactions and corporate governance can be summarized as two main categories of **shareholders** and **executives**, centering on the key object "**Shares**", in terms of the creation, reviewing and voting on a series of motions on corporate governance behaviors, where the **investment agreement** and the **shareholders' agreement** are the two special ones. The **investment agreement** summarizes the conditions and processes of share transactions as batch scripted "**transaction objects**" and fixes them for reviewing and voting at the general meeting. The **shareholders' agreement** is a general articles of the rules and terms of corporate governance, regulating shareholding transactions, the nomination and election of executives, consideration payments, the **shareholders' agreement** updates, and all kinds of corporate governance behaviors.

<figure><img src="../../.gitbook/assets/00-00 EntityRelationship (1).jpg" alt=""><figcaption><p>Diagram of Key data object relationship</p></figcaption></figure>



{% content-ref url="share-and-sharesrepo.md" %}
[share-and-sharesrepo.md](share-and-sharesrepo.md)
{% endcontent-ref %}

{% content-ref url="member-and-membersrepo.md" %}
[member-and-membersrepo.md](member-and-membersrepo.md)
{% endcontent-ref %}

{% content-ref url="position-and-officersrepo.md" %}
[position-and-officersrepo.md](position-and-officersrepo.md)
{% endcontent-ref %}

{% content-ref url="motion-and-motionsrepo/" %}
[motion-and-motionsrepo](motion-and-motionsrepo/)
{% endcontent-ref %}

{% content-ref url="deal-and-dealsrepo/" %}
[deal-and-dealsrepo](deal-and-dealsrepo/)
{% endcontent-ref %}



## 2. Listing of Equity Shares&#x20;

The so-called "**Listing of Equity Shares**" refers to the equity transaction mechanism designed by the system to match transaction in bidding with **fixed-price delegate orders** as the listing objects. The **Listing Rules** of the Shareholders' Agreement may authorize specific classes of shares to be issued and transferred by public bid listing. Once the reviewing and voting is passed, the relevant **listing rules** will come into effect, the company may list additional new shares, and the relevant shareholders may continue to list relevant class of shares after the expiration of the lock-up period.

Only **investors** who are verified the **Real Name** can buy the listed shares, and the person who can review the investor's identity information is the authorized identifier provided in the **Listing Rules**. The total number of investors is also set in the **Listing Rules**, and once the limit is reached, no new investors can be approved to join. The number of potential investors is a core element in determining "**public offering**" or "**open market trading**" in many countries, therefore the company shall determine the maximum number of investors in accordance with the relevant securities laws and regulations and commercial arrangements, and comply with the relevant **reporting and disclosure requirements** in accordance with the law.

Each **sell order object** stipulates the delegation **validity period**, once the validity period expires, the system will automatically withdraw of the expired sell order in the next matching. The delegates can also take the initiative to withdraw the order from the listed **Golden Chain Table** after the expiration of the validity period.

The **listing shares** are all transferable by listing offering, while the conditions of the offering transaction such as **total offering amount**, **maximum offering price**, **minimum price**, and **transaction price** can be stipulated in detailed **Listing Rules**.

The Delegated **sell orders** will be listed in **lowest to highest** order **from beginning to end** in **Golden Chain Table**. Investors can call a specific API to issue a price, issue a delegate buy order with fixed-amount and pay **ETH** as consideration, the system will match the orders in accordance with the "**price priority, time priority** " rules. In the valid delegate period, the sell order with the lowest price will be matched with the buy order, as long as the price of the sell order is less than or equal to the buy order. The amount of sold orders will be reduced accordingly, or totally removed from the Gold Chain Table until the buy order amount is exhausted, or until no more sell orders can be found at the right price. If there is a balance, the system will automatically return it to the investor's **ETH account** with the company for the **investor** to retrieve it on his/her own, which can prevent the re-entry attacks.

After the deal is taken off, the related **sell order** will be deleted directly from the **golden chain table**, but the system will keep the transaction log of the **successful deal**.



<figure><img src="../../.gitbook/assets/15-00 Listing .jpg" alt=""><figcaption><p>Listing Transaction structure</p></figcaption></figure>

{% content-ref url="order-and-ordersrepo.md" %}
[order-and-ordersrepo.md](order-and-ordersrepo.md)
{% endcontent-ref %}



## 3. Equity Pledge and Pledge Transactions

Shareholders can create a pledge on their holding shares to secure the realization of a particular debt at their discretion. In a share pledge relationship, there are three roles involved: creditor, debtor and pledgor. The creditor can transfer the claim, thus the attached pledge is transferred to a third party as well; if the pledgor is the debtor, the creditor can also set a hash lock on the pledge, thus facilitating the debtor to pay off the debt off-chain in order to unlock the private key, and then the debtor will release the pledge with the private key; the debtor can pay the ETH on chain to pay off the debt, simultaneously, the system will calculate and release the pledge in proportion the paid-in contribution, and partially restore the credit limit of the pledged equity. Once the parties reach an agreement on debt extension, the pledgor can call the API to extend the pledge period to reflect the corresponding agreement.





<figure><img src="../../.gitbook/assets/16-00 Pledge.jpg" alt=""><figcaption><p>Pledge repo and the relationship with other entities</p></figcaption></figure>

{% content-ref url="pledge-and-pledgesrepo.md" %}
[pledge-and-pledgesrepo.md](pledge-and-pledgesrepo.md)
{% endcontent-ref %}



## 4. Options and Perfection

The **Options** refers to **Compulsory Purchase Options** and **Compulsory Sell Options** defined through the **Options Terms** of the **Shareholders Agreement**, which are automatically installed in the **Register of Options** after the **Shareholders Agreement** is activated by passing in the General Meeting. The right holder can trigger the exercise of rights after the triggering conditions are fulfilled.

The trigger conditions may include the time factors such as the **rights exercise period**, and also include off-chain data (up to three sets) through condition objects. Therefore, parties may consider external data such as business income, net profit as the triggering conditions for **Compulsory Purchase Options** and **Compulsory Sell Options**, so as to realize special investor rights and interests such as "**valuation adjustment**" or "**rights of first refusal clearance**".

The system adopts the creation and execution of **Swap Contracts** to fulfill **Compulsory Purchase Options** and **Compulsory Sell Options**.

Specifically, when the **Compulsory Sell Options** is exercised, the right holder may select specific shares held by the obligor as "**Pledged Shares**" to create a **Swap Contract** with its own "**underlying shares**". The Obligor may choose to pay ETH as the compulsory purchase options price to acquire the underlying shares, otherwise, the right holder may execute the Swap to acquire the Pledged Shares as netting (difference between the compulsory purchase options price and the underlying shares issuance price) to terminate the Swap.

At the time of exercising the **Compulsory Purchase Options**, the right holder may select the " underlying shares" that meet the agreed category of the **Option Contract** held by the obligor to set up the swap, and at the same time, the system will automatically lock the **underlying shares** so that the right holder will not be able to transfer shares within the paid-up amount of the **Option Contract**. Afterwards, the right holder may choose to pay ETH as the consideration for the **Underlying Shares** (i.e., realizing the **Compulsory Purchase Option**), otherwise, once the validity period of the **Swap Contract** has expired, the obligor may terminate the **Swap Contract** in order to release the lock of the **Underlying Shares**.



<figure><img src="../../.gitbook/assets/17-01 PutOption.jpg" alt=""><figcaption><p>Transaction structure of compulsory sell option</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/17-02 CallOption.jpg" alt=""><figcaption><p>Transaction structure of compulsory purchase option</p></figcaption></figure>

{% content-ref url="option-and-optionsrepo.md" %}
[option-and-optionsrepo.md](option-and-optionsrepo.md)
{% endcontent-ref %}



## 5. **Rules and terms of the Shareholders Agreement**

The rules of corporate governance and share transactions stipulated in a **shareholders agreement** are categorized into "**rules**" and "**terms**" according to their complexity and regulatory matters. **"Rules**" are defined in a 32-bit array and rely on the "**Rules Parser Repository**" to parse the key attribute values, periods values or conditional determination thresholds for each rule, which include: **general corporate governance rules, voting rules, executive position allocation rules, rights of first refusal rules, concert party rules**, and **listing and trading rules**. **"Terms"**, defined by independent smart contracts that rely on structured data objects and their methods to define specific exercise conditions and intermediate parameter algorithms. Currently these include: **anti-dilution terms, lock-up terms, drag-along terms, tag-along terms**, and **(compulsory buy, compulsory sell) options**.

{% content-ref url="rule-and-rulesparser.md" %}
[rule-and-rulesparser.md](rule-and-rulesparser.md)
{% endcontent-ref %}

{% content-ref url="anti-dilution.md" %}
[anti-dilution.md](anti-dilution.md)
{% endcontent-ref %}

{% content-ref url="lock-up.md" %}
[lock-up.md](lock-up.md)
{% endcontent-ref %}

{% content-ref url="drag-tag-along.md" %}
[drag-tag-along.md](drag-tag-along.md)
{% endcontent-ref %}

{% content-ref url="put-call-options.md" %}
[put-call-options.md](put-call-options.md)
{% endcontent-ref %}

