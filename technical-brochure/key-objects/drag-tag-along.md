# 🚜 Drag / Tag Along

### **Function and Usage**&#x20;

**Drag-along term** refers to the right holder compels the obligor to follow him/her in transferring a specific number or percentage of shares to a specific buyer on the same terms and conditions, if the triggering conditions are fulfilled. **Tag-Along term** refers to the right holder is obliged to follow the seller of the share interest to transfer a specific amount or a specific percentage of share interest to a specific buyer under the same terms and conditions, if the triggering conditions are fulfilled. In the event that the right holder exercises the right, the buyer of the original transaction may choose to accept both the **drag-along** and **tag-along** arrangements, and thus buy the underlying shares, otherwise, all the other transactions will not be settled.

In terms of triggering conditions, the transfer of control can serve as a triggering event, and the time requirement, such as an exercise period, can also be added as a triggering condition. Certainly, there may be no specific triggering conditions at all. In such cases, drag-along and tag-along arrangements can be established as a special investment equity that can be exercised unconditionally by the right holder.

### **Members and Attributes**&#x20;

The **tag-along and drag-along** terms define the share transaction linking objects and the **share transaction linking mapping table** with the structure "share seller user number -> share transaction linking objects".

The members of the **(share transaction) linking object** include a **link rule object** and a list of follower's user numbers. Among them, the **link rule object** is defined in the **rule parser repo**, and its attributes are mainly the triggering conditions of the drag-along and tag-along arrangement; the follower refers to the obligor who is required to follow and sell the share in the drag-along arrangement, and the right holder who can request to sell the share in the tag-along arrangement.

The seller of the share is the search key in the drag-along and tag-along arrangements, and can obtain the triggering conditions, exercise rules and counterparties of the relevant arrangement by user number.



**Linking rules**

<figure><img src="../../.gitbook/assets/21-01 LinkRule.jpg" alt=""><figcaption><p>Structure of Linking Rules Object</p></figcaption></figure>

**Meaning of linking Rules of Attributes**

| **Attribute**       | **Commercial and Legal Meaning**                                                                                                                                              |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| triggerDate         | Trigger date.                                                                                                                                                                 |
| effectiveDays       | Number of effective days.                                                                                                                                                     |
| triggerType         | Trigger condition categories. 0-unconditional trigger, 1-transfer of control, 2-transfer of control and price above threshold, 3-transfer of control and ROE above threshold. |
| shareRatioThreshold | The minimum shareholding for company control ( unit: basis points).                                                                                                           |
| rate                | Rate. Category 2 refers to the transfer price; Category 3 refers to the annualized ROE.                                                                                       |
| proRata             | Whether or not to exercise the right at the voting ratio if the right holder claims a conflict.                                                                               |

### **(Share Transaction) Linking Object**

<figure><img src="../../.gitbook/assets/21-02 LinkRule.jpg" alt=""><figcaption><p>(Share Transaction) Linking Object</p></figcaption></figure>

### **(Share Transaction) Linking Object Repo**

<figure><img src="../../.gitbook/assets/21-03 LinksRepo.jpg" alt=""><figcaption><p>(Share Transaction) Linking Object Repo</p></figcaption></figure>

## **Query API**

| **API Name** | **Function and Usage**                                                                                                                                            |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| isDragger    | Query whether a user with a specific number is an share seller with a drag-along and tag-along term.                                                              |
| getLinkRule  | Query the corresponding share transaction linking rule by share seller's user number.                                                                             |
| isFollower   | Query whether a user with a specific number is a follower of a seller with a specific number.                                                                     |
| getDraggers  | Query to get a list of all seller numbers under the drag-along and tag-along term.                                                                                |
| getFollowers | Query to get a list of all follower's numbers for a specific numbered seller.                                                                                     |
| priceCheck   | Query whether the price of a specific transaction for a particular investment agreement meets the minimum price or minimum ROE requirements of the Linking Rules. |
| isTriggered  | Query whether a specific transaction for a specific investment agreement triggers a drag-along and/or tag-along term.                                             |

## Source Code

#### [RulesParser](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/RulesParser.sol) | [LinksRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/LinksRepo.sol) | [Alongs](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/books/roc/terms/Alongs.sol)&#x20;



