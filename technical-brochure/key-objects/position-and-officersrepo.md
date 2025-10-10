# 💺 Position and OfficersRepo

## **Function and Usage**

[**OfficersRepo**](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/OfficersRepo.sol) is a public library that defines the **positions objects** such as directors and managers, as well as the creation, deletion, dismissal, position-taken, resignation, and other changes to the positions. It is worth noting that positions is different from titles, and several different positions may be assigned to the same title (e.g. "Director"). In addition, the system has designed **group objects**, which makes it easy to aggregate and distinguish users' **positions** with the **title** of director, and establish company executive body - the Board of Directors.

## **Members and Attributes**

The members of the **officers repo** include **position objects**, adapting a **position mapping** with "Position Number -> Position Object" structure, a **user position mapping** with "User Number -> Position List" structure, as well as two **position groups**, Director Group and Manager Group.

## **Position Object**

**Position object** is similar to a special "Role", identified by the position number as the main key, while the user number and title are the attributes of the position object. In this way, when a manager takes a position, the user number attribute of a specific position is set to a specific user number. If a user takes multiple positions, the user’s number is equal to the user number of several positions.

<figure><img src="../../.gitbook/assets/08-01 Position.jpg" alt=""><figcaption><p>Position Objects Structure</p></figcaption></figure>



## **The Attribute List of Shareholder Objects**

| Attribute        | Commercial and Legal meaning                                           |
| ---------------- | ---------------------------------------------------------------------- |
| title            | Title:1-Shareholder, 2-Chairman, 3-Vice Chairman, 4-Managing Director… |
| seqOfPos         | Position Number                                                        |
| acct             | User Number of candidate                                               |
| nominator        | User number of nominator                                               |
| startDate        | The start date of position                                             |
| endDate          | The end date of position                                               |
| seqOfVR          | Rule number of voting rule.                                            |
| titleOfNominator | The title of nominator                                                 |



## **Group**

Considering that the board of directors often has some decision-making power as the executive body in the company, the position group objects have been set up to distinguish the **directors group** and the **manager group** without the director role.

<figure><img src="../../.gitbook/assets/08-02 PosGroup.jpg" alt=""><figcaption><p>职位分组结构</p></figcaption></figure>

**Attribute List of Members objects**

| Attribute | Commercial and Legal Meaning  |
| --------- | ----------------------------- |
| posList   | List of positions             |
| acctList  | User number of the candidates |

### Officers Repo

<figure><img src="../../.gitbook/assets/08-03 OfficerRepo.jpg" alt=""><figcaption><p>Officers Repo Structure</p></figcaption></figure>

#### Attributes List of Officers Repo

| Attribute | Commercial and Legal meaning                                                                                                       |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| positions | Positions List                                                                                                                     |
| posInHand | List of officer’s positions. Query all position numbers list held by an officer by user number.                                    |
| directors | Directors Group. Summarizes a list of all directors and the user numbers of the users who hold the position.                       |
| managers  | Managers Group. Summarizes a list of all managers positions other than director and the number of the user who holds the position. |

## Query API

The query API well describes the function and use of the **Officers Repo** in the whole system, as shown in the list below.

| API                     | Function and Usage                                                                    |
| ----------------------- | ------------------------------------------------------------------------------------- |
| posExist                | Query whether a position with a specific number exists.                               |
| isOccupied              | Query whether a position with a specific number is already occupied.                  |
| getPosition             | Gets the position objects for the specified number.                                   |
| getFullPosInfo          | Get an array of related position objects by the number list.                          |
| isManager               | Query whether a user with a specific number is a manager.                             |
| getNumOfManagers        | Query the total number of users in the Manager group.                                 |
| getManagersList         | Get a list of all manager user numbers.                                               |
| getManagersPosList      | Get a list of all manager position numbers.                                           |
| getManagersFullPosInfo  | Get a list of all Manager position objects.                                           |
| isDirector              | Query whether a user of a specific number is a director.                              |
| getNumOfDirectors       | Get the number of directors.                                                          |
| getDirectorsList        | Get a list of director user numbers.                                                  |
| getDirectorsPosList     | Get a list of all director position numbers.                                          |
| getDirectorsFullPosInfo | Get a list of all director position objects.                                          |
| hasPosition             | Query whether a specific user takes specific positions.                               |
| getPosInHand            | Get a list of all positions held by a specific user.                                  |
| getFullPosInfoInHand    | Get a list of all position objects for a specific user.                               |
| hasTitle                | Query whether a user has specific title.                                              |
| hasNominationRight      | Query whether a specific user holds a specific nomination rights.                     |
| getBoardSeatsQuota      | Get the number of nomination seats on the board of directors held by a specific user. |
| getBoardSeatsOccupied   | Get the number of board nomination seats already occupied by a specific user.         |

## Source Code

#### [OfficersRepo](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/lib/OfficersRepo.sol)

