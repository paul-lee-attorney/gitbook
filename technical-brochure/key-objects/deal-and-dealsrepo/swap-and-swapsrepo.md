# 🔄 Swap and SwapsRepo

## **Functions and Usages**&#x20;

**Swap object** is a special transaction object designed by the system to ensure the effective fulfillment of special options agreed by the shareholders agreement, such as **compulsory purchase option** and **compulsory sell option**.&#x20;

When exercising the **compulsory purchase option**, the right holder can directly lock the "underlying shares" through the swap contract, so that without the cooperation of the obligor, it can directly trigger the specific API to change the registration of the underlying shares in its own name. In the case of exercising a **compulsory sell option**, the right holder can set the specific shares held by the obligor as "pledged shares" through the swap contract, so that when the obligor does not pay the consideration, the right holder can trigger the specific API to change the registration of the pledged shares in its own name, and use the value of the pledged shares to make up for the possible profit in the case of a normal exercise of the **compulsory sell option**.&#x20;

In the system, only the shares booked in the share register can be used as security for performance, so the system has designed a swap contract in order to ensure that the **compulsory purchase option** and **compulsory sell option** can logically close the loop of the transaction during the performance process, while the pricing and quantity of the specific pledged shares can be automatically calculated according to **option terms** as agreed in the **shareholders agreement**.

## **Member and Attributes**&#x20;

The members of the **Swaps Repo** include **swap objects** and the **swap mapping** which adopts the structure of "Swap Number -> Swap Object".

### Swaps Objects

<figure><img src="../../../.gitbook/assets/09-02 Swap.jpg" alt=""><figcaption><p>Structure of Swaps Objects</p></figcaption></figure>

#### **Attribute List of Swaps Objects**

| Attribute    | Commercial and Legal Meaning                                 |
| ------------ | ------------------------------------------------------------ |
| seqOfSwap    | Number of swap transaction.                                  |
| seqOfPledge  | Number of Pledged Shares.                                    |
| paidOfPledge | The amount of pledged paid-in contribution.                  |
| seqOfTarget  | Number of underlying shares.                                 |
| paidOfTarget | The amount of paid-in contribution of the underlying shares. |
| priceOfDeal  | Consideration of deal.                                       |
| isPutOpt     | Whether the transaction is a compulsory sell.                |
| state        | The state of the swap transaction.                           |

## **Query API**

The Query API well describes the functions and uses of the **Swaps Repo** in the whole system, see the table below.

| API Name         | Commercial and Legal Meaning                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------ |
| counterOfSwaps   | Get the current value of the Swap Transaction Counter.                                                                   |
| sumPaidOfTarget  | Get the total amount of paid-in contribution for the underlying share.                                                   |
| isSwap           | Query whether a swap transaction with a specific number exists.                                                          |
| getSwap          | Get the swap transaction object with a specific number.                                                                  |
| checkValueOfSwap | Query the total value of the consideration for a particular numbered swap transaction at a specific fiat currency price. |
| getAllSwaps      | Get a list of all swap objects                                                                                           |
| allSwapsClosed   | Query whether all swap transaction have been closed.                                                                     |

## Source Code

#### [SwapsRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/SwapsRepo.sol)

