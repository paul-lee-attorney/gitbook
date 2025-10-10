# 🔄 Condition and ConsRepo

### **Function and Usage**&#x20;

**Condition Object** is a data structure specially used for **comparison** and **boolean** operation. It can store up to 3 comparison parameters and compare 3 sets of data simultaneously, and then perform boolean operation on the comparison results in accordance with the predefined logic, so as to realize and check the complex triggering conditions.



### **Members and Attributes**&#x20;

The main members of the **conditions repo** are the comparison objects and the Comparison mapping which with the structure of "Number -> Comparison Objects".



### Comparison Objects

<figure><img src="../../.gitbook/assets/11-01 Cond.jpg" alt=""><figcaption><p>Comparison Objects</p></figcaption></figure>

#### **Attributes List of Comparison Objects**

| Attribute | Commercial and Legal Meaning       |
| --------- | ---------------------------------- |
| seqOfCond | Condition object number.           |
| logicOpr  | Logical operator (see below).      |
| compOpr1  | Comparison operator-1 (see below). |
| para1     | Comparison parameter-1.            |
| compOpr2  | Comparison operator-2.             |
| para2     | Comparison parameter-2.            |
| compOpr3  | Comparison operator-3.             |
| para3     | Comparison parameter-3.            |

**Value Meaning of Logical Operator Attribute**

| Value | Meaning                            |
| ----- | ---------------------------------- |
| 1     | And（a && b）                        |
| 2     | Or（a \|\| b）                       |
| 3     | Equal to（a == b）                   |
| 4     | Unequal to（a != b）                 |
| 5     | And twice（ a && b && c ）           |
| 6     | Or twice（a \|\| b \|\| c）          |
| 7     | And & Or（a && b \|\| c）            |
| 8     | Or & And（a \|\| b && c）            |
| 9     | Equal to twice（a == b == c）        |
| 10    | Unequal to twice（a != b != c）      |
| 11    | Equal to & Unequal to（a == b != c） |
| 12    | Unequal to、Equal to（a != b == c）   |
| 13    | And & Equal to（a && b == c）        |
| 14    | Equal to & And（a == b && c）        |
| 15    | Or & Equal to（a \|\| b == c）       |
| 16    | Equal to & Or（a == b \|\| c）       |
| 17    | Or& Unequal to（a && b != c）        |
| 18    | Unequal to & Or（a != b && c）       |
| 19    | Or & Unequal to（a \|\| b != c）     |
| 20    | Unequal to & Or（a != b \|\| c）     |

**Value Meaning of Comparison Operator Attribute**

| Value | Meaning                 |
| ----- | ----------------------- |
| 1     | Equal to （a == b）       |
| 2     | Unequal to (a != b)     |
| 3     | More (a > b)            |
| 4     | Less（a < b）             |
| 5     | More & Equal to（a >= b） |
| 6     | Less& Equal to（a <= b）  |

### **Query API**

The query API well describes the function and usage of the **Conditions repo** in the whole system, as shown in the table below.

| API               | Commercial and Legal Meaning                                                                                                                                                                      |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| counterOfConds    | Get the current value of the condition object counter.                                                                                                                                            |
| getConds          | Get a list of all condition objects.                                                                                                                                                              |
| checkCond         | Query whether the input data satisfies a comparison condition consisting of a specific comparison operator (compOpr) and a comparison threshold (para).                                           |
| checkSoleCond     | Query whether the input data (data) satisfies the single comparison operation condition specified in the Condition object (Cond).                                                                 |
| checkCondsOfTwo   | Query whether the input two data (data1 and data2) satisfy the triggering conditions defined jointly by two comparison operations and Boolean operators specified by the Condition object (Cond). |
| checkCondsOfThree | Query whether the input three data (data1, data2 and data3) satisfy the triggering condition defined by the condition object (Cond) with the three comparison operations and boolean operators.   |



## Source Code

#### [CondsRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/CondsRepo.sol)

