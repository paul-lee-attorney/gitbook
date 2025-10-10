# 🖋️ Signature and Sigpage

### **Functions and Usages**&#x20;

A **Signature Page** is a component smart contract, by inheriting which **Investment Agreement** and **Shareholders Agreement** can obtain their members, attributes and methods. The **signature page** consists of a number of **signature blank**, each of which is used to sign by a specific party, and each **signature** represents the express consent of parties, while the **signature blank** and the **block number** where the signature is located are the time identifiers, aiming to confirm and query the time information that users have expressively agreed or exercising rights. The signatures of all parties represent the formation of the contract, which is the premise for submission to the general meeting of shareholders. The **signature page** of an **investment agreement** also serves the purpose of **locking** in underlying shares related to the parties. Specifically, when the seller signs the contract, the system will automatically lock the **clean paid-in contribution** of the **underlying share** with the same amount in the **share register**, thus avoiding the situation where one share is traded repeatedly.

For special shareholders' rights that may **increase** the number of **parties** to the investment agreement, such as **drag-along option** and **tag-along option**, the system will automatically **add** the signatures blanks to the **additional signature page**, and add the relevant **signatures** according to the time when the parties **exercise their rights** or **make promises**. Therefore, both the **investment agreement** and the **shareholders' agreement** include two signature pages, the initial signature page and the additional signature page.

### **Members and Attributes**&#x20;

The main members of the **signature page** are the **signature object**, the **signature blank object**, the signature blank mapping with the structure "user number -> signature blank object", and the list of user numbers of the buyer and the seller.

**Signature Blank Objects**

<figure><img src="../../.gitbook/assets/22-01 Blank.jpg" alt=""><figcaption><p>Structure of Signature Blank Object</p></figcaption></figure>

**Attribute List of Signature Blank**

| **Attribute** | **Commercial and Legal Meaning**                    |
| ------------- | --------------------------------------------------- |
| seqOfDeals    | A list of deal numbers associated with the parties. |
| signer        | Signer user number.                                 |
| sigDate       | Signature time.                                     |
| blocknumber   | Signature block number.                             |
| sigHash       | Signature hash value.                               |
| flag          | The reserved attribute.                             |
| para          | The reserved attribute.                             |
| arg           | The reserved attribute.                             |
| seq           | The reserved attribute.                             |
| attr          | The reserved attribute.                             |

**Attribute List of No.0 Signature Blank Object**

| **Attribute** | **Commercial and Legal Meaning**               |
| ------------- | ---------------------------------------------- |
| sigDate       | Time when the contract was circulated to sign. |
| para          | Number of signature blanks.                    |
| arg           | Number of signed signature blanks.             |
| seq           | Number of days in the signature period.        |
| attr          | Number of days in the delivery period.         |

**Signature Page**&#x20;

The signature page consists of a list of buyer user numbers and a list of seller user numbers in an enumerable set structure, and a signature blank mapping using "user number -> signature blank object". The main function is to summarize the number of parties to the contract and the composition of the specific users, as well as the user roles in the transaction (buyer or seller) and the relevant deal number.

<figure><img src="../../.gitbook/assets/22-02 Page.jpg" alt=""><figcaption><p>签字页的结构</p></figcaption></figure>



## **Query API**

The query API well describes the function and usage of the **Signature Page** in the whole system, as shown in the table below.

| **API Name**       | **Commercial and Legal Meaning**                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------- |
| circulated         | Query whether the contract has been circulated for signature ( circulation time > 0).           |
| established        | Query whether the contract has been formed (number of signature blank == number of signatures). |
| counterOfBlanks    | Number of signature blank.                                                                      |
| counterOfSigs      | Number of signatures.                                                                           |
| getCirculateDate   | Query the time when the contract was circulated.                                                |
| getSigningDays     | Query the days of signature periods to sign the contract.                                       |
| getClosingDays     | Query the number of days to delivery.                                                           |
| getSigDeadline     | Query the deadline for signing the contract.                                                    |
| getClosingDeadline | Query the delivery deadline.                                                                    |
| isSigner           | Query whether the user with the specified number is a signer.                                   |
| sigOfParty         | Query the signature blank object for the user with the specified number.                        |
| sigsOfPage         | Query the signature objects of all parties on the signature page.                               |
| sigsOfSide         | Query all signature objects of the buyer or seller.                                             |



## Source Code

#### [SigsRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/SigsRepo.sol) | [SigPage](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/common/components/SigPage.sol)&#x20;



