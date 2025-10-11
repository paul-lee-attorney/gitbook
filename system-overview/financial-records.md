# 💸 9. Financial Records

**ComBoox** adopts **ETH** and **USDC** as special “**general equivalence**” to pay for new share subscription or share transfer consideration. It also allows companies booked in the system to transfer **ETH** / **USDC** respectively, or to pay **ETH** together with calling external smart contracts to pay for the cost or consideration of legal actions.

To facilitate automatic bookkeeping of the financial records of these activities, the system set up special events in the smart contracts of the **General Keeper**, **Sub-Keepers** and **Cashier**, so that the financial records of these payment activities can be retrieved and summarized in real time automatically.

<details>

<summary>9.<strong>1. Exchange Rate</strong></summary>

1. **ETH/Fiat Currency**

When creating registration books in the system, the company concerned can set its book keeping currency. Currently, the following currencies are acceptable to the system: USD, EUR, GBP, JPY and some other fiat currencies of major countries. During the equity transaction, the system will automatically call the **Chain Link Price Feed** service to query the exchange rate between the bookkeeping currency and **ETH**, and then automatically calculate and deliver **ETH** according to the amount of the fiat currency of the transaction, delivery versus payment.



2. **ETH/CBP**

The system offers **CBP** to the public through the smart contract of **Fuel Tank**, at the **ETH/CBP** exchange rate that is determined by the **Owner** of the **Platform**. Currently, the exchange rate is 1:1, which can be retrieved in real time by users.



3. **USDC**

The price of **USDC** is deemed to be always $1.00 per unit.

</details>

<details>

<summary>9.<strong>2. CBP Flow Records</strong></summary>

As an ERC-20 token, CBP's income and expenditure are booked in the Registration Center, which automatically records the sender, recipient and amount of each transaction. Users can further distinguish the CBP payments with respect to their detailed scenarios and reasons according to the identity of the payer and payee. For example, when the payer is "zero" address, it means the Platform minted coins to the payee.

```solidity
event Transfer(address indexed from, address indexed to, uint256 indexed value);
```

</details>

<details>

<summary>9.<strong>3. ETH Flow Records</strong></summary>

It is only **General Keeper** that has API for equity trading transactions to be settled in **ETH**. Therefore, **ETH** paid together with the transaction is also directly received by **General Keeper.** After that, **General Keeper** will route the relevant equity transaction command to the specific **Sub-Keeper**, and the **Sub-Keeper** will further retrieve the involving parties’ user number and calculate their respective attributable amount of **ETH**, and return the relevant information back to **General Keeper**. Finally, **General Keeper** will allocate the **ETH** received to the specific users' deposit account or custody account according to the feedback information from **Sub-Keeper.**

For example, when a buyer pays the consideration of a share transfer deal in **ETH**, **General Keeper** will receive and store the **ETH** paid with the command, and then route the calling command to the **ROA Keeper**, which will calculate the total amount of the share transfer transaction, call the **Chain Link Price Feed** service to query the **ETH** exchange rate at that time, and then send the ETH records booking instruction back to **General Keeper**. Thereafter, **General Keeper** will credit the amount of **ETH** equivalent to the total transaction price to the seller's deposit account as consideration, and credit the amount of **ETH** exceeding the transaction’s consideration to the buyer's deposit account as over paid balance.



1. **ETH Inflow**

For **ETH** paid to the company such as paid-in contributions and equity subscriptions, the **Sub-Keeper** will only record the reason for the payment through the event log, and the **General Keeper** will not allocate such **ETH** to the deposit account or the custody account.

<table><thead><tr><th width="194.74609375" valign="top">Scenario</th><th width="120.28125" valign="top">Sub-Keeper</th><th valign="top">Event</th></tr></thead><tbody><tr><td valign="top">Pay In Contribution for Capital Increase Deal</td><td valign="top">ROA Keeper</td><td valign="top">event PayOffCIDeal(uint indexed caller, uint indexed valueOfDeal)</td></tr><tr><td valign="top">Pay In Capital Contribution</td><td valign="top">ROM Keeper</td><td valign="top">event PayInCapital (uint indexed seqOfShare, uint indexed amt, uint indexed valueOfDeal)</td></tr><tr><td valign="top">Close New Share Issue Order</td><td valign="top">LOO Keeper</td><td valign="top">event CloseBidAgainstInitOffer(uint indexed buyer, uint indexed amt);</td></tr></tbody></table>



2. **ETH Outflow**

Payments of the Company are all subject to the approval of the **General Meeting of Members** or the **Board of Directors** in accordance with the corporate governance process stipulated in the **Shareholders Agreement**, which are essentially the process of implementing the resolutions of the **General Meeting of Members** or the ones of the **Board of Director**s.

<table><thead><tr><th width="184.1817626953125" valign="top">Scenario</th><th width="125.2567138671875" valign="top">Sub-Keeper</th><th valign="top">Events</th></tr></thead><tbody><tr><td valign="top">Payment approved by the General Meeting of Members</td><td valign="top">GMM Keeper</td><td valign="top">event TransferFund(address indexed to, bool indexed isCBP, uint indexed amt, uint seqOfMotion, uint caller)</td></tr><tr><td valign="top">Execute actions approved by the General Meeting of Members</td><td valign="top">GMM Keeper</td><td valign="top">event ExecAction(address indexed targets, uint indexed values, bytes indexed params, uint seqOfMotion, uint caller)</td></tr><tr><td valign="top">Distribute profits</td><td valign="top">GMM Keeper</td><td valign="top">event DistributeProfits(uint256 indexed sum, uint indexed seqOfMotion, uint indexed caller);</td></tr><tr><td valign="top">Payment approved by the Board of Directors</td><td valign="top">BMM Keeper</td><td valign="top">event TransferFund(address indexed to, bool indexed isCBP, uint indexed amt, uint seqOfMotion, uint caller)</td></tr><tr><td valign="top">Execute actions approved by the Board of Directors</td><td valign="top">BMM Keeper</td><td valign="top">event ExecAction(address indexed targets, uint indexed values, bytes indexed params, uint seqOfMotion, uint caller)</td></tr></tbody></table>



3. **ETH Deposit**

&#x20;   **(1) Save To Coffer Function**

The **General Keeper** manages the transfer and accounting activities of **ETH** payments through the function of **Save To Coffer**. This function only records the recipient’s user number, the specific amount and the reason of payment. Among them, the reason of payment is recorded the summary description of the relevant payment reason in the format of Bytes32 in ASCII coding.

```solidity

function saveToCoffer(uint acct, uint value, bytes32 reason) external {
    require(msg.sender == _keepers[4] ||
            msg.sender == _keepers[5] ||
            msg.sender == _keepers[6] ||
            msg.sender == _keepers[7] ||
            msg.sender == _keepers[10], 
        "GK.saveToCoffer: not correct Keeper");
     require(address(this).balance >= _coffers[0] + value,
        "GK.saveToCoffer: insufficient Eth");
     _coffers[acct] += value;
     _coffers[0] += value;
     emit SaveToCoffer(acct, value, reason);
}

```

&#x20;  &#x20;

&#x20;   **(2) Pickup Deposit Function**

**ETH** deposited in a user's deposit account can only be exclusively picked up by such user trough calling the **Pickup Deposit Function** of **General Keeper**, and cannot be misappropriated or withdrawn by any other account.

<pre class="language-solidity"><code class="lang-solidity">
<strong>function pickupDeposit() external isNormal{
</strong>    uint caller = _msgSender(msg.sender, 18000);
    uint value = _coffers[caller];
    if (value > 0) {
    _coffers[caller] = 0;
    _coffers[0] -= value;
    Address.sendValue(payable(msg.sender), value);
    emit PickupDeposit(msg.sender, caller, value);
 } else revert("GK.pickupDeposit: no balance");
}

</code></pre>



&#x20;   **(3) Deposit Reasons**

The **ETH** deposit reasons, the brief description concerned, as well as the corresponding ASCII code are listed as follows:

<table><thead><tr><th width="144.02520751953125" valign="top">Scenario</th><th width="120.6673583984375" valign="top">Sub Keeper</th><th width="173.37353515625" valign="top">Brief Description</th><th valign="top">ASCII Code (Bytes32 in Hex)</th></tr></thead><tbody><tr><td valign="top">Profits Distribution</td><td valign="top">GMMKeeper</td><td valign="top">DistributeProfits</td><td valign="top">0x4469737472696275746550726f66697473000000000000000000000000000000</td></tr><tr><td valign="top">Deposit Sell Order’s Consideration</td><td valign="top">LOOKeeper</td><td valign="top">CloseBidAgainstOffer</td><td valign="top">0x436c6f7365426964416761696e73744f66666572000000000000000000000000</td></tr><tr><td valign="top">Deposit Buy Order’s Overpaid Balance</td><td valign="top">LOOKeeper</td><td valign="top">DepositBalanceOfBidOrder</td><td valign="top">0x4465706f73697442616c616e63654f664269644f726465720000000000000000</td></tr><tr><td valign="top">Deposit Share Transfer Consideration</td><td valign="top">ROAKeeper</td><td valign="top">DepositConsiderationOfSTDeal</td><td valign="top">0x4465706f736974436f6e73696465726174696f6e4f6653544465616c00000000</td></tr><tr><td valign="top">Deposit Share Transfer Overpaid Balance</td><td valign="top">ROAKeeper</td><td valign="top">DepositBalanceOfOTCDeal</td><td valign="top">0x4465706f73697442616c616e63654f664f54434465616c000000000000000000</td></tr><tr><td valign="top">Deposit Paid In Contribution Balance</td><td valign="top">ROMKeeper</td><td valign="top">DepositBalanceOfPayInCap</td><td valign="top">0x4465706f73697442616c616e63654f66506179496e4361700000000000000000</td></tr><tr><td valign="top">Deposit Swap Deal Consideration</td><td valign="top">ROOKeeper</td><td valign="top">DepositConsiderationOfSwap</td><td valign="top">0x4465706f736974436f6e73696465726174696f6e4f6653776170000000000000</td></tr><tr><td valign="top">Deposit Swap Deal Over Paid Balance</td><td valign="top">ROOKeeper</td><td valign="top">DepositBalanceOfSwap</td><td valign="top">0x4465706f73697442616c616e63654f6653776170000000000000000000000000</td></tr><tr><td valign="top">Deposit Rejected Deal Consideration</td><td valign="top">ROOKeeper</td><td valign="top">DepositConsiderOfRejectedDeal</td><td valign="top">0x4465706f736974436f6e73696465724f6652656a65637465644465616c000000</td></tr><tr><td valign="top">Deposit Rejected Deal Overpaid Balance</td><td valign="top">ROOKeeper</td><td valign="top">DepositBalanceOfRejectedDeal</td><td valign="top">0x4465706f73697442616c616e63654f6652656a65637465644465616c00000000</td></tr></tbody></table>



4. **ETH Escrow**

&#x20;   **(1) Escrow ETH**&#x20;

The system allows verified investors to trade the equity shares of the registered companies in the smart contract of **List of ETH Orders** with six types of orders: limited buy order, market buy order, limited sell order, market sell order, limited issue order, and market issue order.&#x20;

When listing a limited buy order, the system needs to deposit the ETH paid by the buyer into the escrow account as margin.&#x20;

When depositing margin, the system still calls the function of **Save To Coffer** of **General Keeper**, except that the buyer's user number will be duplicated twice and linked together as the account holder. This allows different users to be distinguished and prevents the margin from being taken out by the user himself or any other user.

<pre class="language-solidity"><code class="lang-solidity"><strong>// Example of Deposit Margin Algorithm
</strong><strong>uint acct = bid.buyer;
</strong>acct = (acct &#x3C;&#x3C; 40) + acct;
_gk.saveToCoffer(
    acct, bid.consideration,
    bytes32(0x437573746f647956616c75654f664269644f7264657200000000000000000000)
); // CustodyValueOfBidOrder
</code></pre>

&#x20;  &#x20;

&#x20;   **(2) Release ETH**&#x20;

When a sell order or issue order is listed, the system will take the lead in matching the transaction with the existing listed buy orders, and after the transaction is closed, the margin locked up with the buy order will be released to the seller's deposit account as consideration, or to the company as capital contribution.

Upon releasing the margin, the **Release Custody** function of **General Keeper** will be called, through the events of which the payer, payee, amount, and reason of the payment will automatically be recorded. Similar to **Save To Coffer**, a summary description of the reason of payment will be saved in ASCII code via a Bytes32 fixed-length array.

```solidity

function releaseCustody(uint from, uint to, uint amt, bytes32 reason) external isNormal {
    require (msg.sender == _keepers[10], "GK.releaseCustody: wrong Keeper");
    uint acct = (from << 40) + from; 
    uint value = _coffers[acct];
    require (value >= amt, "GK.releaseCusotody: insufficient");
    _coffers[acct] -= amt;
    if (to > 0) { _coffers[to] += amt;
    } else { _coffers[0] -= amt;}
    emit ReleaseCustody(from, to, amt, reason);
}
```



&#x20;   **(3) Reason of ETH Escrow**&#x20;

The table below provides a summary of the **Sub-Keeper**, reasons for escrow or releasing **ETH** margin and their ASCII codes.

<table><thead><tr><th width="131.727294921875" valign="top">Scenario</th><th width="112.9090576171875" valign="top">Sub Keeper</th><th width="163.272705078125" valign="top">Brief Description</th><th valign="top">ASCII Code (Bytes32 in Hex)</th></tr></thead><tbody><tr><td valign="top">Deposit Buy Order Margin</td><td valign="top">LOO Keeper</td><td valign="top">CustodyValueOfBidOrder</td><td valign="top">0x437573746f647956616c75654f664269644f7264657200000000000000000000</td></tr><tr><td valign="top">Release Margin to Company</td><td valign="top">LOO Keeper</td><td valign="top">CloseInitOfferAgainstBid</td><td valign="top">0x436c6f7365496e69744f66666572416761696e73744269640000000000000000</td></tr><tr><td valign="top">Release Margin to Seller</td><td valign="top">LOO Keeper</td><td valign="top">CloseOfferAgainstBid</td><td valign="top">0x436c6f73654f66666572416761696e7374426964000000000000000000000000</td></tr><tr><td valign="top">Refund Buy Order Margin</td><td valign="top">LOO Keeper</td><td valign="top">RefundValueOfBidOrder</td><td valign="top">0x526566756e6456616c75654f664269644f726465720000000000000000000000</td></tr></tbody></table>



</details>

<details>

<summary>9.<strong>4. USDC Flow Records</strong></summary>

Only the **USD Keeper** provides API for equity trading transactions in **USDC,** and, **Cashier** holds, receives, forwards, transfers, or distributes the **USDC** paid in connection with these transactions, and is also responsible for recording all such **USDC** payment activities.



1. **USDC Inflow**

For **USDC** paid to the company such as paid-in contributions and equity subscriptions, the **Cashier** will only record the reason for the payment through the event log, and will not allocate such **USDC** to any users' deposit account or escrow account.

```solidity
//Collect USD Function of Cashier
function collectUsd(TransferAuth memory auth, bytes32 remark) external anyKeeper {
    _transferWithAuthorization(auth);
    emit ReceiveUsd(auth.from, auth.value, remark);
}
```



2. **USDC Outflow**

In addition to the **USDC Distribution** scenario, any other **USDC** payments of a company shall also be subject to the approval of the **General Meeting of Members** or the **Board of Directors** in accordance with the corporate governance process stipulated in the **Shareholders Agreement**, which are essentially the process of implementing the resolutions of the **General Meeting of Members** or the ones of the **Board of Directo**rs.

The authorized executor needs to call the function of **ExecAction** or **ExecActionOfGM** of **General Keeper**, so as to further invoke the function of **TransferUSD** of **Cashier** to make the payment.

```solidity
//Transfer USD Function of Cashier
function transferUsd(address to, uint amt, bytes32 remark) external anyKeeper {
    require(balanceOfComp() >= amt, "Cashier.transferUsd: insufficient amt");
    emit TransferUsd(to, amt, remark);
    require(_usd().transfer(to, amt),"Cashier.transferUsd: transfer failed"); 
}
```



3. **USDC Deposit**

&#x20;   **(1) Distribute USD Function**

As the price of **USDC** is deemed to be $1.00 per unit, no balance or change will be generated for payments made in **USDC**. Any consideration or refund will be settled directly to the relevant user’s account.

However, in the event that any **USDC** is distributed by a company to its Members, the corresponding amounts will be allocated under each Member’s user number in a private mapping called "\_lockers". Thereafter, Members may retrieve their allocated deposits at their discretion at any time.

```solidity
//Mapping _lockers and Distribute USD Function of Cashier
mapping(uint => uint) private _lockers;

function distributeUsd(uint amt) external {
    require(msg.sender == address(_gk), "Cashier.DistrUsd: not GK");
    require(balanceOfComp( ) >= amt, "Cashier.DistrUsd: insufficient amt");
    IRegisterOfMembers _rom = _gk.getROM( );
    uint[ ] memory members = _rom.membersList();
    uint len = members.length;
    uint totalPoints = _rom.ownersPoints( ).points;
    uint sum = 0;
    while (len > 1) {
    uint member = members[len - 1];
    uint pointsOfMember = _rom.pointsOfMember(member).points;
    uint value = pointsOfMember * amt / totalPoints;
    _lockers[member] += value;
    _lockers[0] += value;
    sum += value;
    len--;
    }
    _lockers[members[0]] += (amt - sum);
    _lockers[0] += (amt - sum);
    emit DistributeUsd(amt);
}

```



&#x20;   **(2) Pickup USD Function**

**USDC** deposited in a user's deposit account can only be exclusively picked up by such user by calling the Pickup USD Function of the **Cashier**, and cannot be misappropriated or withdrawn by any other account.

```solidity
//Pickup USD Function
function pickupUsd() external {
    uint caller = _msgSender(msg.sender, 18000);
    uint value = _lockers[caller];

    if (value > 0) {
        _lockers[caller] = 0;
        _lockers[0] -= value;
        emit PickupUsd(msg.sender, caller, value);
        require(_usd().transfer(msg.sender, value), 
            "Cashier.PickupUsd: transfer failed");
    } else revert("Cashier.pickupDeposit: no balance");
}
```



4. **USDC Escrow**

&#x20;   **(1) Escrow USDC**

The system allows verified investors to trade the equity shares of the registered companies in the smart contract of **List of USD Orders** with six types of orders: limited buy order, market buy order, limited sell order, market sell order, limited issue order, and market issue order. When listing a limited buy order, the system needs to deposit the **USDC** paid by the buyer into the escrow account as margin.

When depositing margin, the system will call the function of **Custody USD** of **Cashier**, and deposit the relevant amount into a private mapping called “\_coffers”. This allows different users to be distinguished and prevents the margin from being taken out by the user himself or any other user.

<pre class="language-solidity"><code class="lang-solidity"><strong>//Function Custody USD of Cashier
</strong><strong>mapping(address => uint) private _coffers;
</strong>
function _transferWithAuthorization(TransferAuth memory auth) private {
        _usd().transferWithAuthorization(
        auth.from, 
        address(this), 
        auth.value,
        auth.validAfter, 
        auth.validBefore, 
        auth.nonce, 
        auth.v,
        auth.r,
        auth.s
    );
}

function custodyUsd(TransferAuth memory auth, bytes32 remark) external anyKeeper {
        _transferWithAuthorization(auth);
        _coffers[auth.from] += auth.value;
        _coffers[address(0)] += auth.value;
        emit CustodyUsd(auth.from, auth.value, remark);
}
</code></pre>



&#x20;   **(2) Release USDC**

When a sell order or issue order is listed, the system will take the lead in matching the transaction with the existing listed buy orders, and after the transaction is closed, the margin locked up with the buy order will be released to the seller's deposit account as consideration, or to the company as capital contribution.

Upon releasing the margin, the **Release USD** function of **Cashier** will be called, through the events of which the payer, payee, amount, and reason of the payment will automatically be recorded. Similar to **Save To Coffer**, a summary description of the reason of payment will be saved in ASCII code via a Bytes32 fixed-length array.

```solidity
//Release USD Function
function releaseUsd(address from, address to, uint amt, bytes32 remark) external anyKeeper {
    require(_coffers[from] >= amt, "Cashier.ReleaseUsd: insufficient amt");
    _coffers[from] -= amt;
    _coffers[address(0)] -= amt;
    emit ReleaseUsd(from, to, amt, remark);
    require(_usd().transfer(to, amt), "Cashier.releaseUsd: transfer failed");
}
```

&#x20;  &#x20;

&#x20;   **(3) Reason of USDC Escrow**

The table below provides a summary of the reasons for escrow or releasing **USDC** margin and their ASCII codes.

<table><thead><tr><th width="143.27264404296875" valign="top">Scenario</th><th width="176.0909423828125" valign="top">Brief Description</th><th valign="top">ASCII Code (Bytes32 in Hex)</th></tr></thead><tbody><tr><td valign="top">Deposit Buy Order Margin</td><td valign="top">CustodyValueOfBid</td><td valign="top">0x437573746f647956616c75654f66426964000000000000000000000000000000</td></tr><tr><td valign="top">Release Margin to Company</td><td valign="top">CloseInitOfferAgainstBid</td><td valign="top">0x436c6f7365496e69744f66666572416761696e73744269640000000000000000</td></tr><tr><td valign="top">Release Margin to Seller</td><td valign="top">CloseOfferAgainstBid</td><td valign="top">0x436c6f73654f66666572416761696e7374426964000000000000000000000000</td></tr><tr><td valign="top">Refund Buy Order Margin</td><td valign="top">RefundValueOfBidOrder</td><td valign="top">0x526566756e6456616c75654f664269644f726465720000000000000000000000</td></tr></tbody></table>



</details>

### Source Codes

#### [RegCenter](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/center/RegCenter.sol)  |  [GeneralKeeper](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/GeneralKeeper.sol)  |  [Cashier](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/books/cashier/Cashier.sol)&#x20;
