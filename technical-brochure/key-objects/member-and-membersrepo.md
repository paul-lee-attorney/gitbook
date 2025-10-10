# 👨‍👨‍👧‍👧 Member and MembersRepo

## **Functions and Usage**

[**MembersRepo**](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/MembersRepo.sol) is a public library that aggregate the information on the **historical status of capital contribution**, **share class**, and **voting weight ranking** of each shareholder. The nature of **Members Repo** is a derivative mapping of the **share mapping** with selected information, changing with the updates in share book-entry system.

## **Members and Attributes**

The **Members Repo** applies three special data structures, one is a **historic state sequence** for tracking the change history in shareholders' contributions; the second one is a **Top Chain** for tracking the voting weight rankings of shareholders and concert actors; and the third one is an **enumerable set**, which tracks list information such as share number list, share class number list.

The members of the **Members Repo** include a **shareholder mapping** with the structure of "user number->shareholder object", a **shareholder ranking chain** using the **top chain** structure, and the **class shareholder number list** with the structure of "share class number->shareholder user number list" structure.

## **Member Objects**

Essentially, the **member object** is a query mapping that obtained by filtering and aggregated the **shareholders, share classes and update time** in the **share mapping**, which facilitates the system to quickly and accurately query specific share states by specific conditions during the operation.

<figure><img src="../../.gitbook/assets/04-01 Member (1) (1).jpg" alt=""><figcaption><p>Member Objects Structure</p></figcaption></figure>

#### Attribute List of **Member Objects**

| Attribute       | Commercial and Legal Meaning                                                                                                                                                |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| votesInHand     | The status of shareholders' equity (historical status sequence), i.e. the historical status sequence of contributions, paid-in contribution and clean paid-in contribution. |
| sharesOfClass   | List of share numbers distinguished by class (enumerable sets). The No.0 class is a list of all shares numbers held by shareholders.                                        |
| classesBelonged | The aggregated table of shareholder numbers calculated by share class (enumerable sets).                                                                                    |

**Members Repo**

In addition to the **shareholder mapping**, the **Members Repo** includes two other members, the **shareholder ranking chain** and the **classed shareholder number list**.

The Shareholder Ranking Chain (chain) applies a **top chain** as data structure, specifically designed to filter out the major shareholders by the minimum threshold specified in the **Shareholders Agreement** and to sort out them by their voting weights. When the **Shareholders Agreement** provides that exercising voting rights shall be based on the subscribed contribution, the chain will calculate the **paid-in contribution** multiplied by **voting weights** held by the shareholders and sort the results. When the **Shareholders Agreement** is updated and takes the **paid-in contribution** as the basis of exercising voting rights, the chain will be automatically updated to calculate the voting weights of the shareholders' nodes and sort results correspondingly.

The **classed shareholder numbers list** is classed and aggregated the shareholder (user) numbers by the share class, so that it is easy to retrieve a list of all shareholders (users) numbers holding shares of that class by share class number.

<figure><img src="../../.gitbook/assets/04-02 MembersRepo.jpg" alt=""><figcaption><p>Structure of Members Repo</p></figcaption></figure>

#### **Attribute List of Members Repo**

<table><thead><tr><th width="234">Attribute</th><th>Commercial and Legal Meaning</th></tr></thead><tbody><tr><td>chain</td><td>The rank of shareholders’ voting weights (Top Chain)</td></tr><tr><td>members</td><td>A Member Objects Mapping with a "user number -> Shareholder Object" structure, in which the votesInHand attribute of the No.0 shareholder object tracks the historical information of changes in the company's ownership equity.</td></tr><tr><td>membersOfClass</td><td>The list of member's number classed by shareholder’s category (enumerable sets), in which No.0 class is a list of all member's numbers.</td></tr></tbody></table>

## Query API

The query API well describes the function and use of the **Shareholder Repo** in the overall system, as shown in the table below.

| API                | Function and Usage                                                                                                                                                                                |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| isMember           | Query whether the user is a shareholder of the company according to the user number.                                                                                                              |
| qtyOfMembers       | Get the total amount of shareholders in the company.                                                                                                                                              |
| membersList        | Get the list of all shareholders number.                                                                                                                                                          |
| ownersEquity       | Get the current equity data, i.e., the total amount of paid-in and contributed capital of the company.                                                                                            |
| capAtDate          | Get the historical information of the company's ownership equity, i.e., the total amount of the company's paid-in capital at a certain time in history.                                           |
| equityOfMember     | Obtain current ownership equity information for a specific shareholder, i.e., the amount of the shareholder's contributions, paid-in contribution, clean paid-in contribution, and voting weight. |
| equityAtDate       | Obtain historical ownership equity information for a specific shareholder at a specific time.                                                                                                     |
| votesAtDate        | Get the total value of voting rights for a specific shareholder at a specific time, i.e., capital contribution x voting weight/100.                                                               |
| votesHistory       | Obtain historical data on all changes in the ownership equity of a specific shareholder.                                                                                                          |
| isClassMember      | Verify whether a shareholder is a holder of a specific class of shares.                                                                                                                           |
| classesBelonged    | Get a list of class numbers of all shares held by a specific shareholder.                                                                                                                         |
| qtyOfClassMember   | Get the number of shareholders holding a specific class of shares.                                                                                                                                |
| getMembersOfClass  | Get a list of shareholder (user) numbers for a specific class of shares. The No.0 class points to a list of all shareholders (users) numbers in the company.                                      |
| qtyOfSharesInHand  | Get the total amount of all shares held by a specific shareholder.                                                                                                                                |
| sharesInHand       | Get a list of the number of all shares held by a specific shareholder.                                                                                                                            |
| qtyOfSharesInClass | Get the total amount of shares held by a specific shareholder in a specific category.                                                                                                             |
| sharesInClass      | Get a list of the share numbers for a specific class of shares held by a specific shareholder.                                                                                                    |

## Source Code

#### [MembersRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/MembersRepo.sol)

