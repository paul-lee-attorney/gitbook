# ⏱️ Checkpoints

## **Function and Usage**

**Checkpoints** defines a mapping table consisting of a series of **state check point** objects to track and record the historic state of **subscribed contribution, paid-in** and **clean paid-in contribution**. This allows the system to retrospectively query the states of shareholders' voting rights at a specific time, satisfying the needs of complex decision-making processes.

## **Members and Attribute**

The **historic state sequence** mainly consists of **state check point** objects, and their " number -> object" mapping table, in which the No.0 object is used as a counter, so the valid historic state starts with No.1 object.

## **The State Check Point**

The **State Check Point** consists of five attributes: timestamp, voting weight, subscribed contribution, paid-in contribution, and clean paid-in contribution.

<figure><img src="../../.gitbook/assets/01-03 Checkpoint.jpg" alt=""><figcaption><p>Structure of Check Point Object</p></figcaption></figure>

#### **Attributes List of State Check Point**

| **Attribute** | **Legal and Commercial Meaning**                                                                                                                                                                                                                                            |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| timestamp     | Check point timestamps. A 48-bit timestamps that can support millisecond precision.                                                                                                                                                                                         |
| votingWeight  | Voting weight is a percentage. Each subscribed contribution share represents 100 times the total of voting rights. For example, "100" means per dollar of subscribed contribution represent one vote; "1800" means per dollar of subscribed contribution represent 18 vote. |
| par           | The subscribed contribution amount, which may remain some contributed but unpaid contribution amount.                                                                                                                                                                       |
| paid          | Paid-in contribution is the actually paid-in contribution amount.                                                                                                                                                                                                           |
| cleanPaid     | Clean paid-in contribution amount, which is the amount without any encumbrances such as pledge and transfer.                                                                                                                                                                |

### **Historic State Sequence**

The **historic state sequence** is the "order->object" mapping table of **state check point** objects, and its core value is to quickly query the closest state check point data **at or before** a specific time through compromise method.

<figure><img src="../../.gitbook/assets/01-04 History.jpg" alt=""><figcaption><p>Structure of Historic State Sequence</p></figcaption></figure>

## **Query API**

The query API ideally describes the function and usage of the **historic state sequence** in the whole system, as described in the following table.

| **API Name**    | **Function and Usage**                                                                |
| --------------- | ------------------------------------------------------------------------------------- |
| counterOfPoints | Get the current value of the state check point counter.                               |
| latest          | Get the closest state check point objects.                                            |
| getAtDate       | Get the closest check point object at /or before a specific time.                     |
| pointsOfHistory | Get the all historic state sequence including the counter and all state check points. |

## Source code

#### [Checkpoints](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/Checkpoints.sol)&#x20;

