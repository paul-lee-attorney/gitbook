# 🔤 EnumerableSet

## **Functions and Usage**

**EnumerableSet** is a public library defined by OpenZeplin project team in MIT License, which consists of **an object set** and a set of methods that can be used to store non-repetitive enumerable set in three data types, Bytes32, Address, and Uint. It can determine whether an element is contained in a set based on its value, and also quickly query the total number of elements in the set, a list of all the elements, and even can query the element value by its number.

## **Members and Attributes**

The main members of the **Enumerable Set** include the **Enumerable Set Object** and the set objects of Byte 32 set, Address set, and Uint set derived from its kernel.

### **Enumerable Set**

The object in **Enumerable Set** consists of a variable-length array with a 32-bit and an "element value -> index number" mapping. This structure not only allows you to quickly get the total number of elements in the set and the list of all elements, but also allows you to quickly query the corresponding array element number (index-1) from the mapping based on the element value, so you can determine whether the element has been contained in the set (index>0), and also allows you to quickly locate and delete specific array when deleting an element.

<figure><img src="../../.gitbook/assets/05-01 EnumerableSet (1).jpg" alt=""><figcaption><p>The Structure of Enumerable Set Repo</p></figcaption></figure>

#### Attribute List of Set Object

| Attribute | Commercial and Legal meaning            |
| --------- | --------------------------------------- |
| \_values  | a variable-length array with bytes 32   |
| \_indexes | "element value -> index number" mapping |

## **Query API**

The query API well describes the function and usage of the **enumerable set repo** in the whole system, as shown in the following list.

| API      | Commercial and Legal Meaning                            |
| -------- | ------------------------------------------------------- |
| contains | Query whether the element has been contained in the set |
| length   | Get the total number of elements in the set.            |
| at       | Get the element values according to array number        |
| values   | Get the list of all elements.                           |

## Source Code

#### [EnumerableSet](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/EnumerableSet.sol)

