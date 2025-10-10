# 🗳️ Ballot and BallotsBox

## **Functions and Usages**&#x20;

[**BallotsBox**](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/BallotsBox.sol) is a public library used by the system to track and record the voting process and the voting results on specific motions.

## **Members and Attributes**&#x20;

The main members of the **ballots box** include the ballots and ballots box objects, as well as the **ballot mapping** which adopts the structure of "user number -> ballot" and the **ballots box mapping** which adopts the structure of "Attitude Number -> ballots box".

### Ballots

<figure><img src="../../../.gitbook/assets/07-02 Ballot.jpg" alt=""><figcaption><p>Ballot structure</p></figcaption></figure>

**Attribute List of Ballot**

| Attribute   | Commercial and Legal Meaning                                                                                            |
| ----------- | ----------------------------------------------------------------------------------------------------------------------- |
| acct        | User number of voters.                                                                                                  |
| attitude    | Voting attitude. 1- Support, 2-Against, 3-Abstain.                                                                      |
| head        | The number of users delegated.                                                                                          |
| weight      | The voting weight value delegated.                                                                                      |
| sigDate     | voting date.                                                                                                            |
| blocknumber | The block number of voting.                                                                                             |
| sigHash     | Signature hash value (for the CID index number of the scanned copy of the written ballot uploaded to the IPFS network). |
| principals  | The array of delegate user numbers of the voter.                                                                        |

### **Case**

**Case** is a query mapping formed by filtering and summarizing the **ballot mapping** by voting attitudes, where No. 0 **case** is a aggregated mapping of all voting attitudes.

<figure><img src="../../../.gitbook/assets/07-03 Case.jpg" alt=""><figcaption><p>Case structure</p></figcaption></figure>

#### **Attribute List on Case**

| Attribute   | Commercial and Legal Meaning                     |
| ----------- | ------------------------------------------------ |
| sumOfHead   | The aggregated number of delegate users.         |
| sumOfWeight | The aggregated number of voting weights.         |
| voters      | The array of user numbers of the voters.         |
| principals  | The array of delegate user numbers of the voter. |

**Box**

<figure><img src="../../../.gitbook/assets/07-04 Box (1).jpg" alt=""><figcaption><p>Box structure</p></figcaption></figure>

## **Query API**

The query API well describes the function and usage of the **ballots box** in the whole system, as shown in the table below.

| API               | Commercial and Legal Meaning                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| isVoted           | Query whether the user with a specific number has voted on a specific numbered motion.                       |
| isVotedFor        | Query whether the vote of a user with a specific number on a specific numbered motion is a specific attitude |
| getCaseOfAttitude | Get voting case of specific attitudes. No. 0 is a aggregated data of all votes.                              |
| getBallot         | Get ballot objects of specific users.                                                                        |

## Source Code

#### [BallotsBox](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/BallotsBox.sol)

