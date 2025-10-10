# 📑 Pledge and PledgesRepo

## **Function and Usage**&#x20;

**Pledges Repo** is a public library that defines the pledge objects and its operation methods of adding, deleting, changing, and checking. The parties can complete legal behaviors such as creation, transfer, release, payment, extension of guarantee period and other legal behaviors of the pledge through the API of the general bookkeeper and pledge bookkeeper contract. The system books pledges with a secondary mapping structure of "share number -> pledge number -> pledge objects", and the amount of **clean paid-in contribution** of the underlying shares will be adjusted accordingly to the **pledge amount** when the pledge is created, so that the pledge can be created and executed in multiple rounds on the same underlying shares.

## **Members and Attributes**&#x20;

The members of the **pledges repo** mainly include a pledge objects mapping and a list of sequence of pledge objects.

## **Pledge Objects**&#x20;

**Pledge Objects** define the key element of the **pledge, the underlying shares** and the principle debt, and is divided into two parts: Head mainly defines the index information that will not be altered with the update of the pledge, while Body mainly defines the key element information that may be altered with the change of the pledge.

<figure><img src="../../.gitbook/assets/10-01 Pledge.jpg" alt=""><figcaption><p>Pledge Object Structure</p></figcaption></figure>

#### Attribute List of Pledge Objects

| Attribute      | Commercial and Legal Meaning                                                                          |
| -------------- | ----------------------------------------------------------------------------------------------------- |
| seqOfShare     | The number of underlying shares.                                                                      |
| seqOfPld       | The number of pledge.                                                                                 |
| createDate     | The creation time for the pledge.                                                                     |
| daysToMaturity | The number of days to the maturity date of the main debt.                                             |
| guaranteeDays  | The number of guarantee days.                                                                         |
| creditor       | Creditor.                                                                                             |
| debtor         | Debtor                                                                                                |
| pledgor        | Pledgor (shareholder of the subject shares).                                                          |
| state          | Pledge status. 0 - in drafting, 1 - issued, 2 - locked, 3 - released, 4 - fulfilled, 5 - revoked.     |
| paid           | Pledged paid-in contribution amount.                                                                  |
| par            | Pledged subscribed contribution amount.                                                               |
| guaranteedAmt  | Pledge Amount.                                                                                        |
| preSeq         | The number of the pledge originally assigned in the transfer of the pledge.                           |
| execDays       | Exercise period of the pledge. Currently the system does not set specific functions in the algorithm. |

### Pledges Repo

<figure><img src="../../.gitbook/assets/10-02 PledgesRepo.jpg" alt=""><figcaption><p>Pledges Repo Structure</p></figcaption></figure>

### **Query API**

The query API well describes the function and usage of the **Pledges repo** in the whole system, as shown in the table below.

| API Name          | Function and Usage                                                                                         |
| ----------------- | ---------------------------------------------------------------------------------------------------------- |
| isTriggered       | Query whether the pledge has been triggered (i.e. whether the maturity date of the main debt has expired). |
| isExpired         | Query whether the pledge has expired (i.e. whether the security period has expired).                       |
| counterOfPld      | Query the current value of the pledge number counter on a specific number of shares.                       |
| isPledge          | Query whether a pledge with a specific number exists on a specific numbered shares.                        |
| getSNList         | Gets a list of all pledge numbers in the pledges repo.                                                     |
| getPledge         | Get the objects of a specific numbered pledge on a specific numbered share.                                |
| getPledgesOfShare | Get a list of all pledges on a specific share.                                                             |
| getAllPledges     | Get a list of all pledge objects in the repo.                                                              |

## Source Code

#### [PledgesRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/PledgesRepo.sol)

