# 🥇 GoldChain

## **Functions and Usages**

**Golden Chain** defines a chain consisting of a series of **order nodes** representing the sell orders for the shares listed for sale, with the nodes sorted in order from the lowest to the highest transfer price. Investors can call a specific API to issue a fixed price **delegation buy orders** and pay **ETH** as consideration, the system will match the sell order in the delegation valid period with the buy order with the lowest price as per the "**price first, time first**" principle. As long as the sell order price is less than or equal to the buy order, the order will be sold at the sell order price, and the closed order will be adjusted to the number of transactions or fully removed from the golden chain until the amount of the buy order is depleted, or no more sell order can be found at the right price. If there is a balance, the system will automatically return the investor's ETH account for the investor to retrieve, aiming to prevent re-entry attacks. Each **sell order object** provides delegation **validity period**, once the validity period expires, the system will automatically in the next aggregation of the expired sell order to do the withdrawal processing; the delegate can initiate to withdraw the specific sell order from the listing of the golden chain.

All the listing shares can be transferred through listing, while the **total issue amount**, **maximum issue price**, **minimum issue price**, **transaction price** and other transaction conditions can be detailedly stipulated in the listing rules.

After the transaction is closed, the relevant **sell order** will be directly deleted from the **golden chain**, but the system will keep the transaction log of the successful transaction in event.

## **Members and Attributes**

The **golden chain** mainly consists of the **node object** representing the sell order of listing shares, and its sell order node mapping chain composed of "node number -> node object".

### **Sell Order Object**

<figure><img src="../../.gitbook/assets/未命名文件 (5) (1).jpg" alt=""><figcaption></figcaption></figure>

### **Attributes List of Sell Order**

<table><thead><tr><th width="214.90911865234375">Attributes</th><th>Commercial and Legal Meaning</th></tr></thead><tbody><tr><td> prev</td><td> The number of previous sell order node.</td></tr><tr><td> next</td><td> The number of next sell order node.</td></tr><tr><td> seqOfShare</td><td>The number of underlying shares of the sell order.</td></tr><tr><td> paid</td><td>The paid-in contribution of the sell order.</td></tr><tr><td> price</td><td> The transaction price of the sell order.</td></tr><tr><td> expireDate</td><td> The expiration date of the sell order.</td></tr><tr><td> isOffer</td><td> Whether the order is a sell order.</td></tr><tr><td> classOfShare</td><td> Number of underlying shares class.</td></tr><tr><td> groupRep</td><td> The user number of representative of buyer's Concert Group</td></tr><tr><td> votingWeight</td><td> The voting weight of the underlying shares.</td></tr><tr><td> distrWeight</td><td> The voting weight of the underlying shares.</td></tr><tr><td> margin</td><td> The margin of the sell order.</td></tr><tr><td> isEth</td><td> Whether the order is settled by ETH.</td></tr><tr><td> Date</td><td> Whether the order is matched and closed.</td></tr></tbody></table>

### **Parameter Objects**&#x20;

The **Parameter object** is mainly used to track the head and tail user numbers of the **minority shareholder** queue, as well as some aggregated data.

<table><thead><tr><th width="214.90911865234375">Attribute</th><th>Commercial and Legal Meaning</th></tr></thead><tbody><tr><td>tail</td><td>The tail node user number of the minority shareholder queue.</td></tr><tr><td>head</td><td>The head node user number of the minority shareholder queue.</td></tr><tr><td>maxQtyOfMembers</td><td>Upper limit on the number of shareholders in the company. 0 - Unlimited number.</td></tr><tr><td>minVoteRatioOnChain</td><td>Major Shareholder Voting Weight Threshold. 10,000 points, i.e., 500 represents 5%.</td></tr><tr><td>qtyOfSticks</td><td>Total number of independent minority shareholders and minority shareholders acting in concert group.</td></tr><tr><td>qtyOfBranches</td><td>Total number of independent major shareholders and major shareholders acting in concert group.</td></tr><tr><td>qtyOfMembers</td><td>Total number of shareholders.</td></tr></tbody></table>

### **Golden Chain**

<figure><img src="../../.gitbook/assets/12-02 GoldChain.jpg" alt=""><figcaption><p>Golden Chain Structure</p></figcaption></figure>



## Query API

The query API well describes the function and usage of the **Golden Chain** in the whole system, as shown in the table below.

| API        | Commercial and Legal Meaning                                         |
| ---------- | -------------------------------------------------------------------- |
| counter    | Get the current value of the node number counter of sell order.      |
| length     | Get the length of the chain, i.e. the sum of all sell order numbers. |
| head       | Get the head node, i.e. the lowest sell order price.                 |
| tail       | Get the tail node, i.e. the highest sell order price.                |
| isNode     | Query whether the specific numbered sell order exists.               |
| getNode    | Get the node object of the specific sell order number.               |
| getSeqList | Get a list of all sell order numbers.                                |
| getChain   | Get a list of all sell order node objects.                           |

<br>

## Source Code

#### [GoldChain](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/GoldChain.sol)

