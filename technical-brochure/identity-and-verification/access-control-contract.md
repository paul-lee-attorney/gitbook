# 🚷 Access Control Contract

## **Function and Usage**

**Access control contract** is a component smart contract for writing operation access control at the smart contract's level, and all smart contracts in the system inherit its members, attributes and methods. Based on the **roles repo**, the **access control contract** adds three special roles, namely, **direct bookkeeper**, **register center** and **general bookkeeper**, which provide identity verification and access control tools through a series of modifier interfaces to control specific writing operation functions at the contract level.

Specifically, the **register contract** directly applies **access control contract modifiers** that require a specific number of **sub-bookkeeper** to access specific writing instructions functions; while all writing instructions functions of **sub-bookkeeper** require that only the **direct bookkeeper** can access, and their **direct bookkeepers** are configured as **general bookkeepers**. This control method allows the system to strictly limit the routing of writing instructions within the system, ensuring that the commercial and legal arrangement can be strictly realized.

## **Members and Attributes**

{% content-ref url="role-and-rolesrepo.md" %}
[role-and-rolesrepo.md](role-and-rolesrepo.md)
{% endcontent-ref %}

**Members and Meaning of Access Control Contracts**

| Members     | Commercial and Legal Meaning        |
| ----------- | ----------------------------------- |
| \_ATTORNEYS | Attorney Role group Name (bytes32). |
| \_dk        | Direct bookkeeper account address.  |
| \_rc        | Register Contract API.              |
| \_gk        | General bookkeeper contract API.    |

## **Modifier API**

| Modifier         | Commercial and Legal Meaning                                                                                     |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| onlyOwner        | Only the owner defined in the roles repo can access.                                                             |
| onlyDK           | Only the direct bookkeeper defined in the Roles Repo can access.                                                 |
| onlyGC           | Only General Counsel (i.e. bookkeeper of the Attorney Role Group as defined in the roles repo) can access.       |
| onlyKeeper       | Only bookkeeper (Direct bookkeeper and Sub-bookkeeper registered in the general bookkeeper contract) can access. |
| onlyAttorney     | Only members of the Attorney Role Group defined in the Roles Repo can access.                                    |
| attorneyOrKeeper | Only attorneys or bookkeepers can access.                                                                        |

## **Query API**

| getOwner     | Query the owner's account address.                         |
| ------------ | ---------------------------------------------------------- |
| getDK        | Query the account address of the direct bookkeeper.        |
| isFinalized  | Query whether the state of contract is "finalized".        |
| getRoleAdmin | Query the bookkeeper account address with a specific role. |
| hasRole      | Query the account address with a specific role.            |

## Source Code

#### [Ownable](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/center/access/Ownable.sol) | [AccessControl](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/common/access/AccessControl.sol)&#x20;





