# ⚖️ Option and OptionsRepo

### **Functions and Usages**&#x20;

The **Options Repo** is a public library that defines the **option objects** and their operation methods for adding, deleting, changing, and checking.

The **Options** refers to **Compulsory Purchase Options** and **Compulsory Sell Options** defined through the **Options Terms** of the **Shareholders Agreement**, which are automatically installed in the **Register of Options** after the **Shareholders Agreement** is activated by passing in the General Meeting. The right holder can trigger the exercise of rights after the triggering conditions are fulfilled.

The trigger conditions may include the time factors such as the **rights exercise period**, and also include off-chain data (up to three sets) through condition objects. Therefore, parties may consider external data such as business income, net profit as the triggering conditions for **Compulsory Purchase Options** and **Compulsory Sell Options**, so as to realize special investor rights and interests such as "**valuation adjustment**" or "**right of first refusal clearance**".

The system adopts the creation and execution of **Swap Contracts** to fulfill **Compulsory Purchase Options** and **Compulsory Sell Options**.

Specifically, when the **Compulsory Sell Options** is exercised, the right holder may select specific shares held by the obligor as "**Pledged Shares**" to create a **Swap Contract** with its own "**underlying shares**". The obligor may choose to pay ETH as the compulsory purchase options price to acquire the underlying shares, otherwise, the right holder may execute the swap to acquire the pledged shares as netting (difference between the compulsory purchase options price and the underlying shares issuance price) to terminate the swap.

At the time of exercising the **Compulsory Purchase Options**, the right holder may select the " underlying shares" that meet the agreed category of the **Option Contract** held by the obligor to set up the swap, and at the same time, the system will automatically lock the **underlying shares** so that the right holder will not be able to transfer shares within the paid-up amount of the **Option Contract**. Afterwards, the right holder may choose to pay ETH as the consideration for the **Underlying Shares** (i.e., realizing the **Compulsory Purchase Option**), otherwise, once the validity period of the **Swap Contract** has expired, the obligor may terminate the **Swap Contract** in order to release the lock of the **underlying Shares**.

<figure><img src="../../.gitbook/assets/17-01 PutOption.jpg" alt=""><figcaption><p>Perfection of Put Option</p></figcaption></figure>



<figure><img src="../../.gitbook/assets/17-02 CallOption.jpg" alt=""><figcaption><p>Perfection of Call Option</p></figcaption></figure>



### **Members and Attributes**

The members of the **options repo** include **option objects** and their **exercise record objects**, as well as an **option mapping** composed of the option number as the query key and an **exercise record mapping** and a list table of option numbers.

### **Condition objects**

{% content-ref url="../structure-and-components/condition-and-consrepo.md" %}
[condition-and-consrepo.md](../structure-and-components/condition-and-consrepo.md)
{% endcontent-ref %}

### **Option Object**

The **option object** includes two key attributes, Head and Body, which define all the elemental information required in the establishment and execution process of the **Compulsory Purchase Options** and **Compulsory Sell Options**, respectively. At the same time, a condition object attribute is reserved in the option object to flexibly input various types of off-chain data as option triggering conditions.

<figure><img src="../../.gitbook/assets/11-02 Option 2.jpg" alt=""><figcaption><p>Structure of Option Objects</p></figcaption></figure>

#### **Attribute List of Option Objects**

| Attributes      | Commercial and Legal Meaning                                                                                                                                                                                                                                                                                                           |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| seqOfOpt        | The number of option.                                                                                                                                                                                                                                                                                                                  |
| typeOfOpt       | Option Type. 0-Price of compulsory buy option, 1-Price of compulsory sell option, 2-ROE Compulsory buy option, 3-ROE compulsory sell option, 4-Compulsory buy option with price condition, 5-compulsory sell option with price condition, 6-ROE Compulsory buy option with condition, and 7-ROE Compulsory sell option with condition. |
| classOfShare    | Class of share.                                                                                                                                                                                                                                                                                                                        |
| rate            | Option rate. The price at which the equity is traded (unit is cent) in the case of price options; the annualized ROE ratio (unit is "one in a ten-thousand", i.e., "basis points") in the case of ROE options.                                                                                                                         |
| issueDate       | Option Issuance Point.                                                                                                                                                                                                                                                                                                                 |
| triggerDate     | The point at which the exercise period begins.                                                                                                                                                                                                                                                                                         |
| execDays        | The number of days in the exercise period.                                                                                                                                                                                                                                                                                             |
| closingDays     | The number of days in the closing period (after exercise).                                                                                                                                                                                                                                                                             |
| obligor         | The user number of obligor.                                                                                                                                                                                                                                                                                                            |
| closingDeadline | Closing deadline of delivery.                                                                                                                                                                                                                                                                                                          |
| rightholder     | The user number of right holders.                                                                                                                                                                                                                                                                                                      |
| paid            | The amount of the paid-in shares of option.                                                                                                                                                                                                                                                                                            |
| par             | The amount of the subscribed shares of option.                                                                                                                                                                                                                                                                                         |
| state           | The state of the option. 0-Preparing, 1-Issued, 2-Executed, 3-Delivered.                                                                                                                                                                                                                                                               |
| cond            | Trigger conditions of the option. Defined as structured "condition Objects" that can bring triggering conditions that up to 3 sets of comparison calculations and 2 sets of boolean calculation.                                                                                                                                       |

### **Exercise Record Object**&#x20;

As the name suggests, the usage of the **exercise record object** is to record the performance of an **option**, which mainly consists of the **obligors set**, **swap repo** adopting an enumerable set structure, and the **external triggering data** adopting a **historic state sequence** structure.

<figure><img src="../../.gitbook/assets/11-03 Record.jpg" alt=""><figcaption><p>Structure of Exercise Record Object</p></figcaption></figure>



#### The Attribute List of Exercise Record Objects

| obligors | The number list of obligors (enumerable sets).              |
| -------- | ----------------------------------------------------------- |
| swaps    | Swap repo.                                                  |
| oracles  | historic state sequence of external trigger condition data. |

## Options Repo

The **options repo** mainly consists of an **options mapping** and an **exercise record mapping** with the **option number** as the query key and the **option object** and exercise record object as the value, respectively, as well as a list of **options' numbers** with an **enumerable set structure**.

<figure><img src="../../.gitbook/assets/11-04 OptionsRepo.jpg" alt=""><figcaption><p>Structure of Options Repo</p></figcaption></figure>

## **Query API**

The query API well describes the function and usage of the **Options repo** in the whole system, as shown in the table below.

| API                   | Function and Usage                                                                                                             |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| counterOfOptions      | Get the current value of the option number counter.                                                                            |
| qtyOfOptions          | Get the total number of option objects.                                                                                        |
| isOption              | Query whether an option object with a specific number exists.                                                                  |
| getOption             | Get the option objects of a specific number.                                                                                   |
| getAllOptions         | Get the list of all option objects.                                                                                            |
| isRightholder         | Query whether a user with a specific number is the right holder of an option with a specific number.                           |
| isObligor             | Query whether a user with a specific number is an obligor of an option with a specific number.                                 |
| getObligorsOfOption   | Get a list of all obligor numbers for an option with a specific number.                                                        |
| getSeqList            | Get a list of all the option numbers in the options repo.                                                                      |
| counterOfSwaps        | Get the current value of the Swap Contract Counter for a specific numbered option.                                             |
| sumPaidOfTarget       | Gets the total amount of paid-in contribution for the underlying share of all swap contracts under a specific numbered option. |
| isSwap                | Query whether a swap contract with a specific number exists for an option with a specific number.                              |
| getSwap               | Obtain the swap contract object of a specific number under a specific numbered option.                                         |
| getAllSwapsOfOption   | Get a list of all swap contracts under a specific numbered option.                                                             |
| allSwapsClosed        | Query whether all the swap contracts under a specific option number have closed.                                               |
| getOracleAtDate       | Get the state of the external trigger data for a specific date for a specific number of options.                               |
| getLatestOracle       | Get the state of the most recent external trigger condition data for an option with a specific number.                         |
| getAllOraclesOfOption | Get the historic state sequence of all external trigger condition data for a specific option number.                           |
| checkValueOfSwap      | Query the value (in ETH) of a specific numbered swap under a specific numbered option at a specific fiat currency price.       |

## Source Code

#### [OptionsRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/OptionsRepo.sol)

