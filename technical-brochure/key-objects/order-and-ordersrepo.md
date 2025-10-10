# 📈 Order and OrdersRepo

## **Function and Usage**

The so-called "**Listing Orders**" refers to the equity transaction mechanism designed by the system to match transaction in open bidding with **fixed-price delegate orders** as the listing objects. The **Listing Rules** of the Shareholders' Agreement may authorize specific classes of shares to be issued and transferred by public bid listing. Once the reviewing and voting is passed, the relevant **listing rules** will come into effect, the company may list additional new shares, and the relevant shareholders may continue to list relevant class of shares after the expiration of the lock-up period.

Only **investors** who are verified the **Real Name** can buy the listed shares, and the person who can review the investor's identity information is the authorized identifier provided in the **Listing Rules**. The total number of investors is also set in the **Listing Rules**, and once the limit is reached, no new investors can be approved to join. The number of potential investors is a core element in determining "**public offering**" or "**open market trading**" in many countries, therefore the company shall determine the maximum number of investors in accordance with the relevant securities laws and regulations and commercial arrangements, and comply with the relevant **reporting and disclosure requirements** in accordance with the law.

Each **sell order object** stipulates the delegation **validity period**, once the validity period expires, the system will automatically withdraw of the expired sell order in the next matching. The delegates can also take the initiative to withdraw the order from the listed **Gold Chain** after the expiration of the validity period.

The **listing shares** are all transferable by listing offering, while the conditions of the offering transaction such as **total offering amount**, **maximum offering price**, **minimum price**, and **transaction price** can be stipulated in detailed **Listing Rules**.

The delegated **sell orders** will be listed in **lowest to highest** order **from beginning to end** in **Gold chain**. Investors can call a specific API to issue a price, issue a delegate buy order with fixed-amount and pay **ETH** as consideration, the system will match the orders in accordance with the "**price priority, time priority**" rules. In the valid delegate period, the sell order with the lowest price will be matched with the buy order, as long as the price of the sell order is less than or equal to the buy order. The amount of sold orders will be reduced accordingly, or totally removed from the Gold Chain until the buy order amount is exhausted, or until no more sell orders can be found at the right price. If there is a balance, the system will automatically return it to the investor's **ETH account** with the company for the **investor** to retrieve it on his/her own, which can prevent the re-entry attacks.

After the deal is taken off, the related **sell order** will be deleted directly from the **Gold Chain**, but the system will keep the transaction log of the **successful deal**.

<figure><img src="../../.gitbook/assets/15-00 Listing .jpg" alt=""><figcaption><p>Relationship Diagram of Listing Order</p></figcaption></figure>



### **Members and Attributes**&#x20;

The members of the **sell orders** **repo** include the **Gold Chain** composed of sell order objects, the investor mapping composed of **investor objects** and variable-length array, and the **closing order chain** and variable-length array composed of closed transaction objects. Although not a member of the **sell orders repo**, the listing rules of the **shareholders agreement** comprehensively stipulate all rules of listing offer and listing transfer.

### **Listing Rules**

<figure><img src="../../.gitbook/assets/15-01 ListingRule (1).jpg" alt=""><figcaption><p>Structure of Listing Rules</p></figcaption></figure>

#### **Attribute List of Listing Rules**

<table><thead><tr><th width="206.00006103515625">Attribute</th><th>Commercial and Legal Meaning</th></tr></thead><tbody><tr><td>seqOfRule</td><td>The Number of rules</td></tr><tr><td>titleOfIssuer</td><td>(Listing offer) Title of the Issuer.</td></tr><tr><td>classOfShare</td><td>The number of share class.</td></tr><tr><td>maxTotalPar</td><td>Maximum amount of subscribed contribution (issued).</td></tr><tr><td>titleOfVerifier</td><td>(Investor) Title of identity verifer.</td></tr><tr><td>maxQtyOfInvestors</td><td>Maximum number of investors.</td></tr><tr><td>ceilingPrice</td><td>Maximum (issue) price.</td></tr><tr><td>floorPrice</td><td>Minimum (issue) Price.</td></tr><tr><td>lockupDays</td><td>Number of lock-up days.</td></tr><tr><td>offPrice</td><td>Price of close order.</td></tr><tr><td>votingWeight</td><td>Voting weight (of issued shares).</td></tr></tbody></table>

### **Sell order object and Gold Chain**

{% content-ref url="../structure-and-components/goldchain.md" %}
[goldchain.md](../structure-and-components/goldchain.md)
{% endcontent-ref %}



### **Deal objects**

<figure><img src="../../.gitbook/assets/副本-未命名文件 (3).jpg" alt=""><figcaption></figcaption></figure>

#### Attribute List of Deal Objects

<table><thead><tr><th width="224">Attributes</th><th width="570.818115234375">Legal and Commercial Meaning</th></tr></thead><tbody><tr><td>buyer</td><td>The user number of buyer.</td></tr><tr><td>groupRep</td><td>The user number of the representative of concerted actor group.</td></tr><tr><td>classOfShare</td><td>Number of underlying shares class.</td></tr><tr><td>seller</td><td>The user number of seller.</td></tr><tr><td>state</td><td>State</td></tr><tr><td>isEth</td><td>Whether the order is settled by ETH.</td></tr><tr><td>isOffer</td><td>Whether the order is a sell order.</td></tr><tr><td>paid</td><td>The amount of paid-in contribution for the close order.</td></tr><tr><td>price</td><td>The transaction price.</td></tr><tr><td>votingWeight</td><td>Voting weight of the underlying shares.</td></tr><tr><td>distrWeight</td><td>Distribution weight of the underlying shares.</td></tr><tr><td>consideration</td><td>The margin paid by buyer.</td></tr></tbody></table>

### **Query API**

The Query API well describes the function and usage of the **Sell Orders Repo** in the overall system, see the table below.

| isInvestor        | Query whether a specific numbered user is an investor.                  |
| ----------------- | ----------------------------------------------------------------------- |
| getInvestor       | Get the investor objects for the specific numbered user.                |
| getQtyOfInvestors | Get the total number of investor objects.                               |
| investorList      | Get a list of all investor user numbers.                                |
| investorInfoList  | Get the list of all investor objects.                                   |
| isClass           | Query whether a specific numbered share class is a listing share class. |
| getClassesList    | Get a list of all listing share classes.                                |
| getExpired        | Get the list of expired sell orders.                                    |
| getDeals          | Get a list of close order objects.                                      |



## Source Code

#### [OrdersRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/OrdersRepo.sol)

