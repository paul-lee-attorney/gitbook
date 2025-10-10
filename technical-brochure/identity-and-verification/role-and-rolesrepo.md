# 😜 Role and RolesRepo

## **Function and Usage**

The **Roles repo** is the basic component of the access control for writing operation at the smart contract's level, and it is also the core member of access control smart contracts. The **roles repo** is the access control of writing instruction for drafting and finalization process of **investment agreements** and **shareholders agreement**. Specifically, a shareholder can create a new contract as the **owner**, then appoint the account with a specific address as an **Attorney**, who can draft the body of the agreement and set the signature page. After the contract is drafted and approved by the shareholder, the shareholder can revoke the appointment of all contract attorneys as the owner of the contract at once and transfer the contract owner to "0 Address", thus finalizing the contract.

## **Members and Attributes**

The **roles repo** mainly defines the **owner** and **role objects**, as well as the **role object mapping** with the structure of "Role Name -> Role Object".

### **Role Objects**

<figure><img src="../../.gitbook/assets/25-01 Role.jpg" alt=""><figcaption><p>Structure of Role Objects</p></figcaption></figure>

**The Attribute Meaning of Role Objects**

| Attribute | Commercial and Legal Meaning                                                    |
| --------- | ------------------------------------------------------------------------------- |
| admin     | The account address of the role bookkeeper.                                     |
| isMember  | Determines whether the account with a specific address is a member of the role. |

### Roles Repo

<figure><img src="../../.gitbook/assets/25-02 RolesRepo.jpg" alt=""><figcaption><p>Structure of Roles Repo</p></figcaption></figure>

#### **The Attribute Meaning of Role Objects**

| Attribute | Commercial and Legal Meaning                                              |
| --------- | ------------------------------------------------------------------------- |
| owner     | Owner account address.                                                    |
| state     | States of the roles repo. 0 - Setting up, 1 - Initialized, 2 - Finalized. |
| roles     | Role mapping. mapping structure: "Role name (bytes32) -> Role object"     |

## **Query API**

The query API well describes the function and use of the **Roles Repo** in the whole system, as shown in the table below.

| getOwner     | Query the owner's account address.                                           |
| ------------ | ---------------------------------------------------------------------------- |
| getRoleAdmin | Query the address of the bookkeeper account for a specific name role.        |
| hasRole      | Query if the account with a specific address is a member of a specific role. |

## Source Code

#### [RolesRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/RolesRepo.sol)



