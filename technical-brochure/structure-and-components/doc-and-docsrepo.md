# 🗄️ Doc and DocsRepo

## **Functions and Usages**&#x20;

Regardless of contract templates or clone contracts, the system regards each smart contract that is tracked and managed as a document, and the **document object** is the data object used to track and record the category, number, template author, creator and other information of these documents.

In the **docs repo**, the system adopts the three-level mapping structure of "template category-> version number-> document number-> document address" to store document address, so that the contract address can be conveniently obtained by category, version and other classification information. Meanwhile, the system also adopts the address mapping with the structure of "document address->document head" to store document query information, so that the contract address of the document can be reversely query for its template category, version, author, creator, and other relevant information.

## **Members and Attributes**&#x20;

The main members of the **docs repo** include the **document objects**, the **document address mapping** with a three-level mapping structure, and the document **query information mapping** with an address mapping structure.

### **File Objects**

<figure><img src="../../.gitbook/assets/24-01 Doc.jpg" alt=""><figcaption><p>Doc Object Structure</p></figcaption></figure>

**Attribute List of Doc Objects**

| Attribute  | Commercial and Legal Meaning            |
| ---------- | --------------------------------------- |
| typeOfDoc  | Document (template) category number.    |
| version    | Document (template) version number.     |
| seqOfDoc   | Document number.                        |
| author     | Document template author.               |
| creator    | Document creator.                       |
| createDate | The time when the document was created. |
| body       | The contract address of the document.   |

### **Docs Repo**&#x20;

In the **Docs Repo**, the system adopts the three-level mapping structure of "template category-> version number-> document number-> document address" to store document address, so that the contract address can be conveniently obtained by category, version and other classification information. Meanwhile, the system also adopts the address mapping with the structure of "document address->document head" to store document query information, so that the contract address of the document can be reversely query for its template category, version, author, creator, and other relevant information.

<figure><img src="../../.gitbook/assets/24-02 DocsRepo.jpg" alt=""><figcaption><p>Docs Repo structure</p></figcaption></figure>

## Query API

The query API well describes the function and usage of the **Docs Repo** in the whole system, as shown in the table below.

| API Name          | Commercial and Legal Meaning                                                                                                    |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| counterOfTypes    | Get the current value of the document category number counter.                                                                  |
| counterOfVersions | Get the current value of the version number counter for a specific document category.                                           |
| counterOfDocs     | Get the current value of the document number counter for a specific document category, specific document version.               |
| getAuthor         | Get the author user number of a contract template for a specific category, specific version.                                    |
| getAuthorByBody   | Query the template author user number for a contract with a specific address.                                                   |
| docExist          | Query whether a document exists for a specific address.                                                                         |
| getHeadByBody     | Query to get the document Head attribute with a specific address.                                                               |
| getDoc            | Query the document object with a specific query number.                                                                         |
| getVersionsList   | Query the list of document objects for all versions of a template for a specific category.                                      |
| getDocsList       | Query the list of document objects with a specific version of a specific category.                                              |
| verifyDoc         | Query whether the clone contract with a specific query number is a clone copy of the relevant version of the template contract. |



## Source Code

#### [DocsRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/DocsRepo.sol)



