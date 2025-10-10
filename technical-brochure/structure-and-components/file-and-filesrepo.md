# 📂 File and FilesRepo

## **Functions and Usages**&#x20;

**FilesRepo** is a component smart contract, by inheriting which **Investment Agreement** and **Shareholders Agreement** can obtain their members, attributes and methods. The **file object** is a data object that tracks and records the contract address, legal effect status, and performance schedule in the contractual smart contracts, such as **investment agreement** and the **shareholders agreement**, and is also the core data object of the **files repo**. Its main function is to ensure the relevant smart contracts can be circulated through the system strictly as per the corporate governance rules and processes stipulated in the **shareholders agreement**, and to ensure that the shareholders' **rights to review motions, voting rights**, as well as the **lock-up period, anti-dilution rights, rights of first refusal, drag-along and tag-along rights, compulsory buy and sell rights**, and other contractual rights, can be strictly implemented during the process of the signing, review, and execution of the agreements.

1. From the time of formation, the **files repo** tracks the contract address and legal effect status of each **shareholders agreement** and **investment agreement**.
2. When finalizing the drafted contract, the **bookkeeper** will analyze the timetable **subject contract** for legal procedures such as signing, proposal, exercise of special shareholder rights (in the case of an **investment agreement**), and voting at the general meeting of shareholders, based on the valid rules of the shareholders agreement at the time and include the timetable in file contract.
3. Subsequently, the **bookkeepers** will check the timetable at each step and control the legal behavior timing of contractual parties, such as signing, voting, and performance, and will update the status of the legal effects of **subject contract** recorded in the **file contracts** when complete each step.

{% hint style="info" %}
For example, when the shareholders submit the **investment agreement** to the general meeting of shareholders for review and vote, the **bookkeeper** will:&#x20;

(1) Call the **investment agreement** folder to query the performance schedule of the subject contract, and calculate and review whether the subject contract is within the exercise period of special shareholder rights such as "right of first refusal" and "tag-along rights" according to the current block timestamp;&#x20;

(2) Create a new general meeting of shareholders motion to submit the subject contract to the general meeting of shareholders for review if there is no such special shareholders' rights arrangement, or the exercise period has expired;

&#x20;(3) At the same time, the legal status of the **subject contract** shall be amended from "formed" to "submitted";&#x20;

(4) If within the exercise period, terminate the submission process of subject contract.
{% endhint %}

### **Members and Attributes**&#x20;

The members of a **files repo** include a **file object mapping** with the structure of "contract address-> file object" and a list of contract addresses with enumerable set structure, which facilitates the system to quickly retrieve and obtain **file objects** based on the contract addresses during operation.

### **File Objects**

<figure><img src="../../.gitbook/assets/23-01 File.jpg" alt=""><figcaption><p>Structure of File Objects</p></figcaption></figure>

**Attribute List of File Objects**

| Attribute         | Commercial and Legal Meaning                                                                                                                     |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| circulateDate     | The time when the file is circulated.                                                                                                            |
| signingDays       | Number of days in file signing period.                                                                                                           |
| closingDays       | Number of closing days for the file.                                                                                                             |
| seqOfVR           | The number of the voting rules applicable to the file.                                                                                           |
| frExecDays        | Number of days for the exercise period of the right of first refusal.                                                                            |
| dtExecDays        | Number of days for the exercise period of the drag-along and tag-along rights.                                                                   |
| dtConfirmDays     | Number of days for the buyer's confirmation period for the drag-along and tag-along rights.                                                      |
| proposeDate       | The time when the motion is submitted to the general meeting of shareholders for review.                                                         |
| invExitDays       | Number of days during which the proposing shareholder withdraws from the investment                                                              |
| votePrepareDays   | Number of days of voting preparation period.                                                                                                     |
| votingDays        | Number of days in the voting period.                                                                                                             |
| execDaysForPutOpt | Number of days of the exercise period for requesting the opposing shareholders to purchase the underlying shares on equal terms (after denying). |
| seqOfMotion       | Number of the motion whose content is the file reviewing.                                                                                        |
| state             | file status (legal validity).                                                                                                                    |
| docUrl            | Storage address online of the contract in natural language ( Recommend IPFS storage, in which docUrl will be file's CID).                        |
| docHash           | The hash value of contract in natural language.                                                                                                  |
| snOfDoc           | A bit-32 array of the Head attribute.                                                                                                            |

**Legal Status of File**

| Status     | Commercial and Legal Meaning                |
| ---------- | ------------------------------------------- |
| Created    | The file has been created.                  |
| Circulated | The file has been circulated for signature. |
| Proposed   | The file has been proposed.                 |
| Approved   | The file has been approved.                 |
| Rejected   | The file has been rejected.                 |
| Closed     | The file has been closed.                   |
| Revoked    | The file has been revoked.                  |

**Files Repo**

The **Files Repo** consists of a **file object mapping** with the structure of "contract address->file object" and a list of contract addresses with enumerable set structure. On the one hand, the address list of all smart contracts tracked by the **files repo** can be conveniently obtained, and on the other hand, the file objects also can be quickly retrieved by contract addresses.

<figure><img src="../../.gitbook/assets/23-02 FilesRepo.jpg" alt=""><figcaption><p>Structure of Files Repo</p></figcaption></figure>

### Query API

The query API well describes the function and usage of the **Files Repo** in the whole system, as shown in the table below.

| API                 | Commercial and Legal Meaning                                                                                                |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| signingDeadline     | Query the signing deadline of the file with specific address.                                                               |
| closingDeadline     | Query the closing deadline of the file with specific address.                                                               |
| frExecDeadline      | Query the deadline of the exercise period of right of first refusal with a specific address.                                |
| dtExecDeadline      | Query the deadline of the exercise period of the tag-along right with a specific address.                                   |
| terminateStartpoint | Query the start point of the termination period of the file with specific address.                                          |
| votingDeadline      | Query the voting deadline of the file with a specific address.                                                              |
| isRegistered        | Query whether the file with specific address is registered in the files repo (i.e. whether it is an object can be tracked). |
| qtyOfFiles          | Query to get the total number of files with tracking records in the files repo.                                             |
| getFilesList        | Query to get the list of all file addresses in the files repo.                                                              |
| getFile             | Query the file object with a specific address.                                                                              |
| getHeadOfFile       | Query the Head attribute of the file object with specific address.                                                          |

## Source Code

#### [FilesRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/FilesRepo.sol) | [FilesFolder](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/common/components/FilesFolder.sol)&#x20;



