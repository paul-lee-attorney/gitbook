# 🖥️ 2. Computational Control Model

**ComBoox** adopts the "**state machine model**" to simulate and control the share transactions and corporate governance activities, specifically:

<details>

<summary><strong>2.1. States</strong></summary>

Information contents of the book-entry registers at each moment are deemed as different **states**, which will be stored in the smart contracts of **Registers** (such as **Register of Shares, Register of Members** and **Meeting Minutes** etc.).

</details>

<details>

<summary><strong>2.2. Transition Process</strong></summary>

Share transactions, corporate governance behaviors and other relevant legal actions are considered as the **transition process** between different **states** of the book-entry **Registers**, and which will be defined and controlled by the smart contracts of **Bookkeepers** with respect to the subject’s identity, action process, terms and conditions, and legal consequences thereof.

![](<../.gitbook/assets/image (3).png>)

</details>

<details>

<summary><strong>2.3. Conditions and Process</strong></summary>

The corporate governance rules (such as voting rules, nomination rules and other rules stipulated in the bylaws or other similar company constitutional documents), as well as the shareholders' special rights (such as First Refusal, Tag-Along and Drag Along,  Anti-Dilution, Put Option and Call Option etc.) are deemed as the **rules, conditions and procedures** to be followed in the **transition process** between the different **states**, and which will be defined by the smart contract of **Shareholders Agreement** with respect to the values of **attributes, duration** or **determination thresholds** for the said rules or rights.  In runtime, **Shareholders Agreement** will timely answer the queries sent from **Bookkeepers** so as to provide parameters to automatically control the execution process of the legal behaviors concerned.

</details>

<details>

<summary><strong>2.4. Write Operation Scripts</strong></summary>

**Investment Agreement** can be deemed as a special script or batch file consisting of a series of write operation commands to cause the states transition of **Register of Shares**. And, the transaction factors defined in **Investment Agreement** as attributes of object **Deal** (such as subject equity, parties concerned, quantities and price etc.) can be deemed as input parameters (or specific trigger events) of the said write operations concerned, which will be executed by the relevant **Bookkeepers** automatically.

</details>



