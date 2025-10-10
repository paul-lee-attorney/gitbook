# ✍️ DelegateMap

## **Functions and Usages**

[**DelegateMap**](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/DelegateMap.sol) is a public library used to track and record the delegation behavior of voting rights holders who appoint representatives and establish delegate relationships during the proposal or voting process for a specific motion.

## **Members and Attributes**

The main members of the **Delegate Map** are the **voter objects** and the **voter mapping** with the structure of "user number -> voter object".

### **Voter objects**

<figure><img src="../../../.gitbook/assets/07-01 Voter.jpg" alt=""><figcaption><p>Voters object structure</p></figcaption></figure>

#### Attribute List of Voters Objects

| Attribute | Commercial and Legal Meaning                                       |
| --------- | ------------------------------------------------------------------ |
| delegate  | The delegate user number of the voter.                             |
| weight    | The voting weight value of the voter.                              |
| repWeight | The total value of the delegated voting weights held by the voter. |
| repHead   | Total number of delegators represented by the voter.               |

## **Query API**

The query API well describes the function and usage of the **Delegate Map** in the whole system, as shown in the table below.

<table><thead><tr><th width="282">API</th><th>Commercial and Legal Meaning</th></tr></thead><tbody><tr><td>getDelegateOf</td><td>Get the delegate with a specific numbered user.</td></tr></tbody></table>

## Source Code

#### [DelegateMap](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/DelegateMap.sol)

