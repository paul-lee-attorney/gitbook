# 🛍️ Deal and DealsRepo

## **Functions and Usages**&#x20;

The [**DealsRepo**](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/DealsRepo.sol) is a public library that defines the **deal object** and its series of operation methods for adding, deleting, changing, and checking. As a script of batch process instructions to change the bookkeeping records, the **Deals Repo** also defines APIs related to the fulfillment of the **investment agreement** such as locking the subject of the transaction, delivering the shares, and terminating the transaction. The **deal object** is the core content of the **investment agreement**, which is set by the agreement attorney at the time of drafting the agreement. After review and approval, the deal object may be dynamically updated under the arrangement of bookkeeper as per the terms of the **Shareholders Agreement** on the the **special investor's rights and interests**, and all the necessary parameters are provided in the agreement's fulfillment to facilitate the update of bookkeeping records.

## **Members and Attributes**&#x20;

The members of the **Deals Repo** include the **transaction mapping** with the **transaction number** as the search key and the **deal object** as the search value, as well as the **swap object** and **swap mapping** designed for the realization of options.

## **Deal Object**&#x20;

The **deal object** defines all the input parameters required to change the **share bookkeeping**, as well as a hash time lock in 32byte, using for by both parties when trade off-chain or pay equity consideration across the chain.

{% hint style="info" %}
The basic transaction logic and common process of **hash time lock** is:

1. The seller sets the **hash function value** as the **share combination lock**, which locks the underlying share, and simultaneously sets the delivery deadline, beyond which the equity is automatically reversed and the delivery arrangement is revoked;
2. The buyer sets the **same hash function value** as the **consideration combination lock** off-chain or across the chain, locks the share transfer consideration (cryptocurrency, central bank digital currency or other programmable digital currency), and at the same time, sets the payment deadline, after which the payment will be reversed and the payment arrangement will be revoked;
3. The seller calls the unlocking API of the **consideration combination lock**, inputs the **source data** for generative hash function value, unlocks the combination lock, and withdraws the consideration for the share transfer;
4. The buyer utilizes the **source data** obtained during the unlocking process of the **consideration combination lock** to unlock the lock, and triggers the automatic registration change process in order to acquire the underlying share.
{% endhint %}

{% hint style="info" %}
There are several key settings to be aware of for **hash time lock** arrangements:

1. Sellers should not hold the authority to revoke a **delivery** arrangement while the **share** combination lock is in effect;
2. The buyer should not hold the authority to revoke the **payment** arrangement while the **payment** combination lock is in effect;
3. the **delivery** deadline should be later than the payment deadline to allow sufficient action time for the buyer to withdraw the equity; and
4. It is recommended to set the counterparties of the share transfer and the consideration payment in the hash lock contract as a specific buyer and a specific payee, so as to avoid a third party from deciphering or intercepting the lock and obtaining the locked-in equity.
{% endhint %}



<figure><img src="../../../.gitbook/assets/09-01 Deal.jpg" alt=""><figcaption><p>Deal Object Structure</p></figcaption></figure>

**Attribute List of Deal Objects**

| Attribute       | Commercial and Legal Meaning                                                                                                                                             |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| typeOfDeal      | Transaction Type: 1-Capital Increase, 2-External Transfer, 3-Internal Transfer, 4-Preemptive, 5-Tag-along, 6-Drag-along, 7-right of first refusal, 8-Anti-dilution Gift. |
| seqOfDeal       | Transaction Number.                                                                                                                                                      |
| preSeq          | The pre-transaction sequence that triggers the automatic created transaction.                                                                                            |
| classOfShare    | Number of underlying share class.                                                                                                                                        |
| seqOfShare      | Number of underlying shares.                                                                                                                                             |
| seller          | Number of transaction seller.                                                                                                                                            |
| priceOfPaid     | The price of paid-in contribution of the underlying shares.                                                                                                              |
| priceOfPar      | The price of the unpaid contribution of the underlying shares.                                                                                                           |
| closingDeadline | Delivery deadline.                                                                                                                                                       |
| votingWeight    | Voting weight of the underlying shares. (Used to create new shares in a capital increase transactions)                                                                   |
| buyer           | Number of transaction buyer.                                                                                                                                             |
| groupOfBuyer    | User number of the representative of the buyer's Concert Group.                                                                                                          |
| paid            | The amount of paid-in contribution of the transaction.                                                                                                                   |
| par             | The amount of contributed amount of the transaction.                                                                                                                     |
| state           | State of the transaction.                                                                                                                                                |
| hashLock        | Transaction Hash Lock. Used to lock and release the shares subject to the transaction when the consideration is paid off-chain.                                          |

### **Swap and Swaps Repo**

{% content-ref url="swap-and-swapsrepo.md" %}
[swap-and-swapsrepo.md](swap-and-swapsrepo.md)
{% endcontent-ref %}

### **Deals Repo**

<figure><img src="../../../.gitbook/assets/09-03 DealsRepo.jpg" alt=""><figcaption><p>Deals Repo Structure</p></figcaption></figure>

## Query API

The query API well describes the function and usage of the **Deals Repo** in the whole system, as shown in the table below.

| API Name            | Function and Usage                                                                                                                        |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| getTypeOfIA         | Query the type of investment agreement.                                                                                                   |
| counterOfDeal       | Query the current value of the transaction number counter.                                                                                |
| counterOfClosedDeal | Query the number of closed transaction.                                                                                                   |
| isDeal              | Query whether a specific transaction exists.                                                                                              |
| getDeal             | Get the specific number transaction object.                                                                                               |
| getSeqList          | Get the numbered list of transaction.                                                                                                     |
| counterOfSwaps      | Get the current value of the swap number counter.                                                                                         |
| sumPaidOfTarget     | Get the total amount of paid-in contribution for the underlying shares of the swap deal corresponding to a specific numbered transaction. |
| isSwap              | Query whether there is a specific numbered swap arrangement for a specific numbered transaction.                                          |
| getSwap             | Get the number of the swap arrangement for a specific numbered transaction.                                                               |
| getAllSwaps         | Get all the swap arrangements corresponding to a specific numbered transaction.                                                           |
| allSwapsClosed      | Query whether all swap transactions have been closed.                                                                                     |
| checkValueOfSwap    | Calculate the transaction value of a specific numbered swaps for a specific numbered deal at a specific fiat currency price.              |
| checkValueOfDeal    | Calculate the transaction value of a specific numbered deal at a specific fiat currency price.                                            |

## Source Codes

#### [DealsRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/DealsRepo.sol)

