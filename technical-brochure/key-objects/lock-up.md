# 🔐 Lock Up

### **Functions and Usages**&#x20;

**LockUp** defines a **locker objects**, which allows to set of a lock-up period and a corresponding unlocking right holder for the specific numbered share. Prior to the expiration of the lock-up period, the underlying share will not be transferable unless all the right holders with unlock rights vote in favor of unlocking at the shareholders' meeting.

Among them, The list of unlock rights holders for No. 0 Period Locker includes the numbers of all locked underlying shares and is available for the system to query a complete number list of the locked shares.

### **Members and Attributes**&#x20;

**The Period Locker term** defines the **period locker objects** and the period lock mapping table with the structure of "Share No. -> Period Lock Objects".

### **Period Locker Objects**

<figure><img src="../../.gitbook/assets/20-01 Locker.jpg" alt=""><figcaption><p>Period Locker Objects</p></figcaption></figure>

#### Meaning of Period Locker Object Attribute

| **Attribute** | **Commercial and Legal Meaning**                                                                                                                                                                                  |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dueDate       | The due date of lock-up period.                                                                                                                                                                                   |
| keyHolders    | List of unlocked rights holders. If all rights holders vote in favor of the share transfer, the period locker term is deemed to be waived and the underlying shares may be transferred during the lock-up period. |

**Period Locker Mapping Table**

<figure><img src="../../.gitbook/assets/20-02 Lockers.jpg" alt=""><figcaption><p>Structure of Period Locker Mapping Table</p></figcaption></figure>

## **Query API**

| **API Name** | **Function and Usage**                                                                                                                      |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| isLocked     | Query whether a lock-up period has been set for a specific numbered share.                                                                  |
| getLocker    | Gets the object of locking period for a specific numbered share.                                                                            |
| lockedShares | Get a list of all locked-in share numbers.                                                                                                  |
| isTriggered  | Query whether the subject shareholding of a specific transaction of a specific investment contract is locked.                               |
| isExempted   | Query whether the lock-up arrangement of the underlying shares of a specific transaction of a specific investment contract has been waived. |

## Source Code

#### [LockUp](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/books/roc/terms/LockUp.sol) | [LockersRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/LockersRepo.sol)&#x20;

