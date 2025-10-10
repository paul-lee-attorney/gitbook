# 🍵 Anti-Dilution

### **Function and Usage**&#x20;

**Anti-Dilution** define the minimum price at which a specific class of shares can be issued, i.e. the floor price. Once the price is lower than the floor price, the obligor (usually the controlling shareholder) should give certain number of shares to the right holder for free in order to lower the right holder's investment cost, enabling the cost of the right holder's investment equal to the lower price of the newly issued shares.

### **Members and attributes**&#x20;

The **Anti-Dilution term** defines the **benchmark price object** and a **price ruler mapping table** using a "share class -> benchmark price object" structure, as well as a list of share class numbers which applies anti-dilution term.

### **Price Benchmark Objects**

<figure><img src="../../.gitbook/assets/19-01 AntiDilution.jpg" alt=""><figcaption><p>Structure of Price Benchmark Objects</p></figcaption></figure>

### **Meaning of Price Benchmark Object Attributes**

| **Attribute** | **Commercial and Legal Meaning** |
| ------------- | -------------------------------- |
| classOfShare  | The number of share class.       |
| floorPrice    | Minimum price.                   |
| obligors      | List of obligor user numbers.    |

### **Price ruler objects**

<figure><img src="../../.gitbook/assets/19-02 Ruler.jpg" alt=""><figcaption><p>Structure of price ruler objects</p></figcaption></figure>

### **Meaning of Price Ruler Object Attributes**

| **Attribute** | **Commercial and Legal Meaning**         |
| ------------- | ---------------------------------------- |
| marks         | Price benchmark object mapping table.    |
| classes       | List of share classes (enumerable sets). |

### **Query API**

| **API Name**         | **Function and Usage**                                                                                                                                                                                     |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| isMarked             | Query whether a specific class of shares has set a minimum limit on the additional issued shares.                                                                                                          |
| getClasses           | Get a list of all the class numbers of shares for which anti-dilution term have been set.                                                                                                                  |
| getFloorPriceOfClass | Get the minimum price for a specific class of shares.                                                                                                                                                      |
| getObligorsOfAD      | Get a list of all obligor user numbers for a specific class of shares.                                                                                                                                     |
| isObligor            | Query whether a specific numbered user is an obligor under the anti-dilution term for a specific class of shares.                                                                                          |
| getGiftPaid          | Calculate the amount of paid-in contribution to be granted for free by the obligor, by additional issue transactions by specific number under specific investment agreements, and underlying share number. |
| isTriggered          | Query whether the anti-dilution term has been triggered by the specific transaction object and the underlying share number.                                                                                |



## Source Code

#### [Anti-Dilution](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/books/roc/terms/AntiDilution.sol)



