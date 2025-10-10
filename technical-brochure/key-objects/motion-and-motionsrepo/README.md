# 🗳️ Motion and MotionsRepo

## **Function and Usage**

[**MotionsRepo**](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/MotionsRepo.sol) is a public library that defines the **motion object**, **voting result object**, and the creation of motions, motions proposal, voting, voting counting, and other legal behaviors related to the **motion object**.

## **Members and Attribute**

The members of the **motions repo** include a **motion mapping** and a **voting result mapping** with a **motion number** as the query key and a **motion object** and a **voting result object** as the query value, respectively, as well as a list of **motion numbers** stored in an **enumerable set**.

### **Motions Objects**

The **motions object** is the core of corporate governance activities, and is the linkage that connects review events such as shareholders' agreements, investment agreements, executive nominations, company actions or payment arrangements with company decision-making activities such as general meeting resolutions and board resolutions. The **motions object** includes four members: Head, Body, VotingRule and Contents.

1. Head: mainly records indexed information that will not be changed after creation, such as the motion category, creator, creation time, etc.;
2. Body: mainly records procedure information such as proposer, proposal date and share registration date.
3. VotingRule: It is the voting object queried from the **Shareholders Agreement** according to the voting rule number when propose a motion, which is used to control the procedure and conditions of the proposal, voting, vote calculation, etc.;
4. Contents: It is the pointer and Linking that connects the **motions objects** to the motion contents.
   * It is used to record the agreement address in reviewing **Shareholder Agreement** and **Investment Agreement**.
   * It is used to record the officer position number when reviewing the nomination of officers;
   * When reviewing a company's on-chain actions, it records the hash value of the a series of target contract address, API, input parameters, token amount, and the other instruction codes; and
   * When reviewing a company's on-chain payment, it records the address of payee, consideration, and other information.

<figure><img src="../../../.gitbook/assets/06-01 Motion.jpg" alt=""><figcaption><p>Structure of Motions Repo</p></figcaption></figure>

#### **Attribute List of Motions Objects**

| Attribute     | Commercial and Legal Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| typeOfMotion  | Type of motion. 1-Elect officers, 2-type of motion, 3- remove officers, 4-review files, 5-review actions, 6-payment for consideration, 7-profits distribution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| seqOfMotion   | Motion number.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| seqOfVR       | Voting rules number.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| creator       | User number of motion creator.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| executor      | User number of motion executor. For specific API in motions, such as corporate behaviors, consideration payment, can only be called by authorized executors.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| createDate    | The date when the motion was created. A 48-bit timestamp, generated at the time the motion was created based on the block timestamp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| proposer      | User number of the proposer of the motion who submit the motions to general meeting or the board of directors.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| proposeDate   | The date when the motion was proposed. A 48-bit timestamp, generated at the time the motion was proposed based on the block timestamp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| shareRegDate  | Share registration date. A 48-bit timestamp, which is generated by the voting rules at the time of proposal. At the time of voting, the shareholder's vote weights are obtained and the voting result is calculated based on this timestamp.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| voteStartDate | The point at which voting begins. A 48-bit timestamp, generated by the voting rules at the time of the proposal.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| voteEndDate   | The point at which voting ends. 48-bit timestamp, generated by the voting rules at the time of the proposal.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| state         | Motion state. 1-Created, 2-Proposed, 3-Passed, 4-Vetoed, 5-Vetoed but not required to subscribe, 6-Vetoed and required to subscribe, 7-Fulfilled.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| votingRule    | Object of the voting rights rules. For details of the members and their meanings, please refer to the voting rights rules in the shareholders' agreement.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| contents      | Contents of Motions. Used to identify or point to the matter to be reviewed, with different formats and meanings for different motion categories, specifically: (1) Motion to elect or remove executives: 16-bit position number; (2) Approval of shareholders' agreement or **investment agreement**: 160-bit smart contract address; (3) Approval of corporate actions: hash value of calling instructions such as the address of the target contract, API, input parameter, and the number of tokens basis to be sent; and (4) Approval of payment or distribution of profits: hash value of several core parameters such as payee address, currency, consideration, valid payment deadline. |

### **Voting Record Object**

The **voting record object** is used to track and record the trajectory of the two legal behaviors of delegation and voting in the voting process, which is also a source of data for the vote counting.

### **Members and Attributes**

The **voting record object** consists of two members: **Delegate Mapping** and **Ballot and Ballot Box**.

{% content-ref url="delegatemap.md" %}
[delegatemap.md](delegatemap.md)
{% endcontent-ref %}

{% content-ref url="ballot-and-ballotsbox.md" %}
[ballot-and-ballotsbox.md](ballot-and-ballotsbox.md)
{% endcontent-ref %}



### Motions Repo

<figure><img src="../../../.gitbook/assets/07-05 MotionsRepo.jpg" alt=""><figcaption><p>Structure of Motions Repo</p></figcaption></figure>



**Query API**

The query API well describes the function and usage of the **Motions repo** in the whole system, as shown in the table below.

| API                   | Function and Usage                                                                                                     |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| isProposed            | Query whether a motion with a specific number is proposed.                                                             |
| voteStarted           | Query whether the voting for a motion with a specific number starts.                                                   |
| voteEnded             | Query whether the voting for a motion with a specific number ends.                                                     |
| getVoterOfDelegateMap | Get the voter object corresponding to the user with a specific number during the review of a specific numbered motion. |
| getDelegateOf         | Get the representative user number for a specific numbered user during the review of a specific numbered motion.       |
| getMotion             | Get the motion objects with specific number.                                                                           |
| isVoted               | Query whether a specific numbered user has voted on a specific numbered motion.                                        |
| isVotedFor            | Query whether the vote of a user with a specific number on a specific numbered motion is a specific attitude           |
| getCaseOfAttitude     | Get the ballot box object for a specific numbered motion with a specific attitude.                                     |
| getBallot             | Get the voting object for a specific numbered user in a specific numbered motion.                                      |
| isPassed              | Query whether a specific numbered motion has passed.                                                                   |
| getSeqList            | Get a numbered list of all motions in motions repo.                                                                    |

## Source Code

#### [MotionsRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/MotionsRepo.sol)

