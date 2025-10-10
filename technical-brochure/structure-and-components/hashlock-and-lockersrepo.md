# 🔐 HashLock and LockersRepo

## **Function and Usage**

The basic principle of **hash lock** is to utilize the **strong collision-free attribute** of the hash function, using the **hash value** as a locker to lock the equity on blockchain, and using the **source data** as a key to trigger the unlocking function (i.e., When the result of the hash operation on the source data is equal to the hash value, the unlock condition is fulfilled.) The equity transferor sets the quantity, transferee, validity period and other information of the underlying shares in the locker function, and then uses the unlocked source data as the private key, and delivers to equity transferee while receiving the consideration off-chain; after obtaining the private key, the transferee inputs the source data on blockchain to trigger the unlocking function if the condition is fulfilled, so that the underlying shares is changed to its own name automatically. In this way, a settlement arrangement can be fully realized whereby the consideration is payed off-chain while the book-entry equity is automatically transferred on-chain. The system's locker has two basic functions, one is to set up the locking function and unlocking function by the principle of hash lock, enabling the user to locker and deliver the book-entry equity on blcokchain; the other function is to add the smart contract address of the consideration locker and unlocking function API to the unlock function of the book-entry equity. In this way, when the equity transferee inputs the private key to locker, the system can synchronize the unlocking of the transaction consideration. When the transferee of the interests enters the private key to unlock, the system can unlock the hash lock of the transaction consideration locker at the same time, so that the same blockchain transaction instruction can unlock the hash locks of the book-entry equity and the transaction consideration simultaneously, enabling synchronized delivery of equity and consideration.

## **Members and Attributes**

The main members of a **locker** are the **locker object**, and the **locker mapping**, which uses a "hash lock -> locker object" structure.

### **Locker Objects**

<figure><img src="../../.gitbook/assets/27-01 Locker.jpg" alt=""><figcaption><p>The Structure of Locker</p></figcaption></figure>

**Attribute List of Locker Objects**

| Attribute     | Commercial and Legal Meaning                                                           |
| ------------- | -------------------------------------------------------------------------------------- |
| from          | User number of share transferor.                                                       |
| to            | User number of share transferee.                                                       |
| expireDate    | Locker expiration date.                                                                |
| value         | Amount of the locked equity.                                                           |
| counterLocker | The address of the locker contract to lock transaction price.                          |
| payload       | Instruction contents that are called by the transaction consideration unlock function. |

### **Lockers Repo**

The members of the **locker** include the **locker mapping** using "hash value --> locker object" and **hash value** list as query keys.

<figure><img src="../../.gitbook/assets/27-02 LockersRepo.jpg" alt=""><figcaption><p>The Structure of Lockers Repo</p></figcaption></figure>

## **Query API**

| API             | Commercial and Legal Meaning                                               |
| --------------- | -------------------------------------------------------------------------- |
| getHeadOfLocker | Query to get the locker Head object corresponding to a specific hash lock. |
| getLocker       | Query to get the locker object corresponding to a specific hash lock.      |
| getSnList       | Query to get a list of all hash locks in the locker.                       |

## Source Code

#### [LockersRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/LockersRepo.sol)



