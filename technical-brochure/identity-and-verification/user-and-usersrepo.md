# 🦸 User and UsersRepo

## **Function and Usage**

Borrowing the concept of distributed digital identity, the **Users Repo** makes full use of the **user number mapping** and the **user object mapping** to register and manage user identities, and simultaneously provides a query API to verify the account identity at any time by a registered contract of ComBoox. When a user exercises the right, the system will call the query API of the **Users Repo** to obtain the account number of the user who issues the instruction, and then verify the user's identity according to the records of the specific **register contract**. For example, when a shareholders exercise voting rights, the system will query the issuer's account number, and then pass it to the **general meeting minutes keeper**, which will query the **Register of Members** to verify whether the user with that number is a shareholder of the company. If the shareholder identity is confirmed, the system will continue; otherwise, it will terminate the operation and return with error message. Before using the ComBoox system's writing function, users should register as a user of the system (registration is not required for only access to company's book-entry information on ComBoox). The Users Repo will assign a unique user number to the registered account address. To prevent the user from losing control if the private key is missed, the system allows registered users to set up an additional account address as a "**backup key**" (the account address assigned by registration is the "**prime key**"). However, in order to prevent the avoidance of contractual obligations such as lock-up periods and first refusal rules, the system prohibits the change of **backup key** or the adding more keys. Therefore, a user can have two accounts at most, one for the **prime key** and one for the **backup key**, and both are interchangeable. Writing instruction sent from the backup key account can also be query with the same user number as the **prime key**. Both the prime key and the backup key can only be associated to only one **user number**, and the used account address cannot be registered another **user number**. The **user number** query API is only open to the registered accounts in the platform and the users themselves, ensuring identity verification while minimizing security risks from external contract access.

## **Members and Attributes**

The Users Repo defines **user objects**, using a **user number mapping** of "account address -> user number" and a **user object mapping** of "user number -> user object".

### **User Objects**

<figure><img src="../../.gitbook/assets/26-01 User.jpg" alt=""><figcaption><p>The Structure of User Objects</p></figcaption></figure>

#### **Members and Meanings of User Objects**

| Member    | Commercial and Legal Attribute  |
| --------- | ------------------------------- |
| primeKey  | The user's prime key object.    |
| backupKey | The user's backup key object.   |
| pubKey    | The account address of the key. |
| discount  | Discount Rate.                  |
| gift      | Gift Points.                    |
| coupon    | Coupon Points.                  |

**Attribute and Meaning of No.0 User**

| Attribute         | Commercial and Legal Meaning                                        |
| ----------------- | ------------------------------------------------------------------- |
| primeKey.gift     | eoaRewards: New User Rewards for registration of external accounts. |
| backupKey.gift    | coaRewards: New User Rewards for registration of internal accounts. |
| backupKey.coupon  | floor: Minimum unit price of the contract template.                 |
| primeKey.discount | rate: Commission discount rate of the platform (in basis points).   |
| primeKey.coupon   | counterOfUsers: Counter of user numbers.                            |

**Users Repo**

<figure><img src="../../.gitbook/assets/26-02 UsersRepo.jpg" alt=""><figcaption><p>Structure of Users Repo</p></figcaption></figure>

## &#x20;Query API

| API Name        | Commercial and Legal Meaning                                              |
| --------------- | ------------------------------------------------------------------------- |
| getPlatformRule | Get Platform (Promotions) rules.                                          |
| getRoyaltyRule  | Get the Royalties ( promotion) rules for a specific user author.          |
| getLocker       | Get the locker object corresponding to a specific hash value.             |
| getLocksList    | Get a list of all hash locks.                                             |
| counterOfUsers  | Get the current counter value of all user numbers.                        |
| getOwner        | Get (Register Center) owner account address.                              |
| getBookeeper    | Get the (Register Center) Bookkeeper account address.                     |
| isKey           | Query whether a specific address is registered in the users repo.         |
| getUser         | Query the user object that corresponds to a specific account address.     |
| getUserNo       | Query to get the user number corresponding to a specific account address. |

## Source Code

#### [UsersRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/UsersRepo.sol)





