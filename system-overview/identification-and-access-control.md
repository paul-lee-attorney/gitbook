# 🚷 Identification and Access Control

The smooth and safe operation of the **system** heavily rely on users' access control and routing control of the write commands.  In other words, for the calling commands which can change the world states ("**write commands**"), it is vital to review and verify the identity and authority of the message sender (i.e. the calling account that send out the commands), and at the same time, the smart contract that received the write commands also needs to strictly control their further routing path, i.e. the target contract's address as well as its API to be further called.  In brief, by strict controlling the write commands' routing path from two directions of "receiving” and “sending", the information of the whole system can be updated as per the predefined commercial and legal logic.

The write commands in the system can be divided into three categories:

1. **System Configuration**: refers to the contracts drafting and system configuration actions triggered by external accounts, which will NOT lead to legal consequences;
2. **Legal Acts**: refers to the share transaction and corporate governance activities triggered by external accounts, which WILL directly lead to legal consequences; and
3. **Algorithmic Control**: refers to the write commands sent by **Bookkeeper**, upon receiving the previous two types of write commands, in accordance with the predefined algorithms of system, in an orderly manner and be able to change the states of other smart contracts like **Registers, Shareholders Agreement**, or **Investment Agreement**.

For the above write commands, the system adopts three verification methods as per their different nature of behaviors and scopes of influence.

<details>

<summary>🚦 Access Control Mechanism on smart contracts' level</summary>

For **System Configuration** and **Algorithmic Control**, these two types of write commands do not dispose any book-entry interests of the system, and usually only take effects within the scope of the company, therefore, belong to the category of technique activities like system configuration, algorithmic control, and operation maintenance. Therefore, **ComBoox** adopts special smart contracts of **Ownable**, **Access Control** and **Draft Control**, which are inheritable and with component attributes, to verify identity of message sender by means of checking their address at the level of each smart contract.

1. **Ownable**

**Ownership** is a reusable, inheritable, component-based smart contract, which specialized in defining address accounts of “**Owner**” and “**Reg Center**”. Clone contracts created through **Reg Center** are descendant of the **Ownership** contract. The address of **Reg Center** cannot be changed once it is set, while the **Owner** can transfer his/her role to other accounts.

2. **Access Control**

A**ccess Control** is a reusable, inheritable, component-based smart contract. Each and every smart contracts of the system are all descendant contracts of **Access Control**, so they all can use the methods and attributes inherited from **Access Control** to define roles with different write permissions and to verify them accordingly. **Access Control** defines two special roles "**Direct Keeper**" and "**General Keeper**”.

**AccessControl** defines two special roles, "**General Keeper"** and "**Direct Keeper"**, as well as a pre-defined role group ---- **Attorneys** (the admin of which is called as "**General Counsel**").

3. **Draft Control**

**Draft Control** is a reusable, inheritable, component-based smart contract designed to define role groupings and their verification logic at the smart contract level. It is a descendant contract of **Access Control** and introduces a specialized role group known as **Attorneys**, whose administrative authority is assigned to a role referred to as the **General Counsel**. Only the EOA having Attorney role may edit or configure the terms of **Investment Agreement** or **Shareholders Agreement**.

Therefore, **Investment Agreement**, **Shareholders Agreement, Alongs, AntiDilution, LockUp,** and **Options** are all descendant contracts of **Draft Control**

4. **Owner**

**Owner** can be initially appointed by the deployer of the contract concerned, and, from the perspectives of commercial and legal, **Owner** usually maps the role of "shareholder" of a company who has the rights to create, propose, review, and approve by voting of the legal documents like contracts, bylaws as well as motions of the General Meeting.

**Owners** can transfer their role to other accounts, and will lose their role as **Owner** thereafter.

**Direct Keeper** is the special role that cannot be influenced by **Owner**, which ensures its relative independence with respect to the roles appointment and control rights assignment, so as to check and balance the power of **Owner** from the perspective of system maintenance or duties independence.

5. **Direct Keeper**

**Direct Keeper** can be initially set by the account deploying of the smart contract, which has special authority to configure system, mapping the role of "Company Secretary" or “Accountants” from the commercial and legal view, the authority design of which reflects the characteristics of “Company Secretary” or “Accountants” who are relatively independent from shareholders and senior executives in system maintenance and assuming independent responsibilities.

**Direct Keeper** can transfer its role to other accounts, and will lose the role of **Direct Keeper** thereafter.

All write APIs of **SubKeepers** are set as only accessible for their **Direct Keepers** or other **SubKeepers**. In this way, all the write authorities will be collectively authorized to **General Keeper** or other **SubKeepers**, thus excluding any external accounts or external contracts out of the system interfering with the company's governance activities, and ensuring that the company's book-entry records can operate securely and automatically, without any human interference involved.

The "**Direct Keeper**" of **General Keeper** has the following special authorities:

1. Set and update the registration address for each **SubKeeper** and **Register**;
2. Appoint or remove the "**Direct Keeper**" for each of the **SubKeeper** and **Register**;
3. Input off-chain "oracle" data (e.g. financial data such as revenue, net profit, etc.) into the system as trigger conditions for exercising certain shareholders rights; and
4. Set up hash lock for pay-in capital, so as for new share subscribers can automatically obtain their Certificates of Contribution upon paying their capital contribution.

Therefore, the characters of its authority are quite similar to "**Company Secretary**" or "**Chief Accountant**".

If **Direct Keeper** of **General Keeper** transfers its role to "zero address", then it means the possibility of human interference with the company's book-entry system is completely abandoned, and the system will automatically operate by smart contracts.  As a cost, such auto-running system cannot be upgraded with new contract templates, neither can use off-chain data as trigger conditions for special rights (like call option or put option) any more.

6. **General Counsel and Attorneys**

**General Counsel** is the admin of the roles group of **Attorneys** and has authorities to grant **Attorney** role to any account addresses.

**Attorneys** can quit their role of **Attorney** by calling the "**RenouceRole**" API, and **General Counsel** can call the "AbandonRole" API to fire all **Attorneys** at once.

For two types of smart contracts, **ShareholdersAgreement** and **InvestmentAgreement**, only **Attorney** can call their write APIs to "draft" the contents of the contracts (such as rules and terms of **ShareholdersAgreement**), or the deal's elements for trading shares (such as the subject share, price, amount), as well as the procedural conditions concerned (such as the contractual parties, signing deadline, and closing deadline).

Therefore, after creating a draft of **ShareholdersAgreement** or **InvestmentAgreement**, the creator as the "**Owner**" needs to appoint a "**General Counsel**" (which can further appoint one or more attorneys) to the contract, who will be responsible for drafting rest of the contents thereof accordingly.  After drafting, **Owner** can review and confirm the contract contents and then calls "**LockContents**" API thereof to fire all attorneys at once and transfers the role of **Owner** to "zero address", so that the contents can no longer be altered manually.

It should be emphasised that if **Owner** does not transfer its role to "zero address",  **Owner** still can modify the contract by reappointing other address as "**General Counsel**" or "**Attorneys"**.

</details>

<details>

<summary>🚏  Commands Routing Mechanism within a company</summary>

A **Register** usually allows several **SubKeepers** to call its write APIs, therefore, it is not economic to rely on **AccessControl** solution to control write authorities among different roles for each of the contracts.  Therefore, **ComBoox** sets up two registration mappings of address in **GeneralKeeper** to satisfy the routing requirements for **Algorithmic Control** commands among the book-entry **Registers** of a company.

There are two special registration mappings of address in the **General Keeper**, which are used to track and record the addresses of "**SubKeepers**" and "**Registers**", and adopt a structure of "sequence number => address" so as to ensure a timely search of the corresponding address as per the sequence number concerned.

When deploying the system, the contract addresses of each **SubKeeper** and **Register** will be input into the registration mappings accordingly, thereafter, in runtime, the relevant write API of **Register** will, before processing the write command received, firstly call **General Keeper** to query and verify whether the message sender’s address equals to the address of the specific contract registered in the mappings, so as to complete the identity verification for the **Algorithmic Control Commands**.

***

For example, the share transfer API of **Register of Shares** will be called by **ROA Keeper** when closing a share transfer transaction, and will also be called by **SHA Keeper** when implementing an Anti-Dilution right. Therefore, **Register of Shares** cannot rely on the unique role of “**Direct Keeper**” defined by **Access Control** to control its write permission, instead, it will query the address mapping of **General Keeper** or **USD Keeper** to check and verify message sender’s identity, i.e. as long as the account address of the caller can match any one of the two contracts mentioned above, the verification will be passed.

</details>

<details>

<summary>🏛️ Users Identification Mechanism for entire system</summary>

**Legal Acts** directly govern the disposal of book-entry interests, carrying significant commercial and legal implications. They may also give rise to relationships with other companies registered within the **ComBoox** system. Accordingly, the platform incorporates a dedicated smart contract, known as the **Reg Center,** along with a suite of methods designed for user identification. These mechanisms ensure robust identity verification across the entire system.

“**Users**” in the platform of **ComBoox**:

(1)      can be shareholders, directors, managers within the Company, or the creditors, delegates, or agents outside of the Company;

(2)      can establish a contractual relationship with one company, or establish legal relationships with multiple companies simultaneously;

(3)      can be a natural person who controls on-chain behaviors through an external account, or a legal person who exercises its corporate legal rights through a contract account.

Therefore, **ComBoox** introduced a special smart contract **Reg Center** to manage all the digital identities of the users.

***

**ComBoox** only takes the account address as the sole label to identify a user, and does not touch the name, nationality, residence or any other social characters of a natural person or a legal person. Therefore, strictly speaking, it is only the "**digital identity**" that the system actually manages or verifies.

This "**de-identified**" identity management model is shaped, on the one hand, by the inherent technical characteristics of public blockchain, and on the other, by its effectiveness in safeguarding users' personal privacy.

<mark style="color:orange;">**Nevertheless, almost all countries have real-name requirements like KYC or anti-money laundering for commercial activities such as investment, financing, lending, payment, and foreign exchange etc.  So please consult with legal experts of the relevant jurisdictions to seek professional advice on securities laws, anti-money laundering laws and other relevant legal issues so as to ensure all the arrangements and activities can be designed and carried out in a legal way.**</mark>

With the concept of distributed digital identity, **Reg Center** uses a special user number mapping to register and manage users' identities, and at the same time, it also provides a query API for all smart contracts of the system to query and verify the users' identity in runtime.

**1. User Number Mapping**

**User Number Mapping** takes a structure as "address => uint(40)", which can be queried via a special API for the corresponding user number with a specific account address.

When users exercise their rights, the **SubKeepers** of the relevant company invoke, through a dedicated middleware smart contract known as **Royalty Charge**, the query API of the **Reg Center**. This **Royalty Charge**, which the **SubKeepers** have inherited, enables them to retrieve the user number of the message sender. The system then verifies the user’s identity and access rights based on the records maintained in the corresponding **Register**.

For example, when shareholders exercise voting rights, **GMM Keeper** of the company will firstly call **Reg Center** to query the user number of the message sender, upon receiving the response, **General Keeper** will pass the returned value of user number along with other input parameters to the **General Meeting Minutes Keeper ("GMM Keeper")**, and **GMM Keeper** will further call **Register of Members** to check whether the user is a member of the company. If the answer is yes, **GMM Keeper** will continue to execute the rest codes accordingly, otherwise, it will terminate the process and return an error message instead.

**2. User Registration**

Before using any write functions of **ComBoox**,  users need to apply for a registration number first (only checking, query or conduct other read operations in **ComBoox** does not require registration).  Then, **RegCenter** will assign a unique user number to the applicant as per its account address automatically.

After creating new book-entry system for a company, the creator may call "Create Corp Seal" API of **General Keeper** to register a specific user number for the company with **Reg Center**. **Reg Center** will then assign a user number to the address of the **General Keeper**, which represents the legal person of the company in **ComBoox** and can be used to send write commands to exercise rights on behalf of the company concerned. (If creating a new book-entry system by calling the "Create Comp" API of **Reg Center**, predefined scripts will automatically register a user number for the new company.)

**3. Backup Key**

To avoid losing the entire account only because of losing private key, **ComBoox** allows the registered users to set **ONE** additional account address as " **Backup Key**" (the account address used in registration process is deemed as "**Prime Key**").  However, to prevent the circumvention of some obligations such as "Lock-Up" or "First Refusal", the system does **NOT** allow to change the **Backup Key** or add more keys.  Therefore, a user can only have a maximum of two keys, the "**Prime Key**" and "**Backup** **Key**".   The address of "**Backup** **key**" can also be recognized by **RegCenter** as having the same user number as the "**Prime Key**".   Any used account address cannot be used again to register user number or set backup key.

**4. Permission for Query User Number**

The query API of **Reg Center** for checking user number is only accessibly for the contract accounts already registered in **ComBoox** and the user's own account. This is to prevent the potential security risks that may be brought by the external contracts' access as much as possible.

</details>



## Source Code

#### &#x20;[Ownable](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/center/access/Ownable.sol) | [AccessControl](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/common/access/AccessControl.sol) | [RolesRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/RolesRepo.sol) | [GeneralKeeper](../) | [UsersRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/UsersRepo.sol)&#x20;
