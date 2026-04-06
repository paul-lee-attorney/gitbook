# 💸 9. Financial Records

**ComBoox** adopts **USDC** as special “**general equivalence**” to pay for new share subscription or share transfer consideration. It also allows companies booked in the system to transfer **USDC** respectively, or to pay **ETH** together with calling external smart contracts to pay for the cost or consideration of legal actions.

To facilitate automatic bookkeeping of the financial records of these activities, the system set up special events in the smart contracts of the **General Keeper**, **Sub-Keepers** and **Cashier**, so that the financial records of these payment activities can be retrieved and summarized in real time automatically.

<details>

<summary>9.<strong>1. Exchange Rate</strong></summary>



1. **USD/CBP**

The system offers **CBP** to the public through the smart contract of **Fuel Tank**, at the **CBP/USD** exchange rate that is determined by the **Owner** of the **Platform**. Currently, the exchange rate is 2,816.15, which can be retrieved in real time by users.



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

<summary>9.3<strong>. USDC Flow Records</strong></summary>

ComBoox provides API for equity trading transactions in **USDC,** and, **Cashier** holds, receives, forwards, transfers, or distributes the **USDC** paid in connection with these transactions, and is also responsible for recording all such **USDC** payment activities.



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

function distrProfits(uint amt, uint seqOfDR) external onlyKeeper returns(
    WaterfallsRepo.Drop[] memory mlist
){    
    if (balanceOfComp() < amt) {
        revert Cashier_Overflow(bytes32("Cashier_InsufficientAmt"));
    }
    RulesParser.DistrRule memory rule =
        _gk.getSHA().getRule(seqOfDR).DistrRuleParser();
    IRegisterOfMembers _rom = _gk.getROM();
    IRegisterOfShares _ros = _gk.getROS();
    WaterfallsRepo.Drop memory drop;
    if ( rule.typeOfDistr == uint8(RulesParser.TypeOfDistr.ProRata)) {
        (drop, mlist, ) = _rivers.proRataDistr(amt, _rom, _ros, false);
    } else if (rule.typeOfDistr == uint8(RulesParser.TypeOfDistr.IntFront)) {
        (drop, mlist, ) = _rivers.intFrontDistr(amt, _ros, rule);
    } else revert Cashier_WrongState(bytes32("Cashier_WrongTypeOfDistr"));
    emit DistrProfits(amt, seqOfDR, drop.seqOfDistr);
    _distrUsd(mlist, bytes32("DistrProfits"));
}

// Book each distribution drop as a deposit for the member.
// `mlist` is the list of drops to deposit; `remark` tags the ledger entry.
function _distrUsd(WaterfallsRepo.Drop[] memory mlist, bytes32 remark) private {
    uint len = mlist.length;
    while (len > 0) {
        WaterfallsRepo.Drop memory drop = mlist[len-1];
        _depositUsd(drop.member, drop.income + drop.principal, remark);
        len--;
    }
}

function distrIncome(uint amt, uint seqOfDR, uint fundManager) external onlyKeeper 
    returns(WaterfallsRepo.Drop[] memory mlist, WaterfallsRepo.Drop[] memory slist){
    if (balanceOfComp() < amt) {
        revert Cashier_Overflow(bytes32("Cashier_ShortOfAmt"));
    }
    RulesParser.DistrRule memory rule = 
       _gk.getSHA().getRule(seqOfDR).DistrRuleParser();
    IRegisterOfMembers _rom = _gk.getROM();
    IRegisterOfShares _ros = _gk.getROS();
    WaterfallsRepo.Drop memory drop;
    if ( rule.typeOfDistr == uint8(RulesParser.TypeOfDistr.ProRata)) {
        (drop, mlist, slist) = _rivers.proRataDistr(amt, _rom, _ros, true);
    } else if (rule.typeOfDistr == uint8(RulesParser.TypeOfDistr.IntFront)) {
        (drop, mlist, slist) = _rivers.intFrontDistr(amt, _ros, rule);
    } else if (rule.typeOfDistr == uint8(RulesParser.TypeOfDistr.PrinFront)) {
        (drop, mlist, slist) = _rivers.prinFrontDistr(amt, _ros, rule);
    } else if (rule.typeOfDistr == uint8(RulesParser.TypeOfDistr.HuddleCarry)) {
        (drop, mlist, slist) = _rivers.hurdleCarryDistr(amt, _ros, rule, fundManager);
    } else revert Cashier_WrongState(bytes32("Cashier_WrongTypeOfDistr"));
    emit DistrIncome(amt, seqOfDR, fundManager, drop.seqOfDistr);
    _distrUsd(mlist, bytes32("DistrIncome"));
}

function depositUsd(uint amt, uint user, bytes32 remark) external onlyKeeper{
    if (balanceOfComp() < amt) {
        revert Cashier_Overflow(bytes32("Cashier_ShortOfAmt"));
    }
    _depositUsd(user, amt, remark);
}

// Credit `amt` USD to the internal deposit locker of `payee`.
// `remark` is an accounting tag for the deposit event.
function _depositUsd(uint payee, uint amt, bytes32 remark) private {
    if (payee == 0) {
        revert Cashier_WrongParty(bytes32("Cashier_ZeroPayee"));
    }        
    emit DepositUsd(amt, payee, remark);
    _lockers[payee] += amt;
    _lockers[0] += amt;
}

```



&#x20;   **(2) Pickup USD Function**

**USDC** deposited in a user's deposit account can only be exclusively picked up by such user by calling the Pickup USD Function of the **Cashier**, and cannot be misappropriated or withdrawn by any other account.

```solidity
//Pickup USD Function
function pickupUsd() external {
    uint caller = _msgSender(0xa019f9ef, 18000);
    uint value = _lockers[caller];

    if (value > 0) {
        _lockers[caller] = 0;
        _lockers[0] -= value;
        emit PickupUsd(msg.sender, caller, value);
        if (!_gk.getBank().transfer(msg.sender, value)) {
            revert Cashier_TransferFailed(bytes32("Cashier_TransferFailed"));
        }
   } else revert Cashier_Overflow(bytes32("Cashier_NoBalance"));
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
function releaseUsd(
    address from, address to, uint amt, bytes32 remark
) external onlyKeeper {
    if(_coffers[from] < amt) {
        revert Cashier_Overflow(bytes32("Cashier_InsufficientAmt"));
    }
    _coffers[from] -= amt;
    _coffers[address(0)] -= amt;
    emit ReleaseUsd(from, to, amt, remark);
    if (!_gk.getBank().transfer(to, amt)) {
        revert Cashier_TransferFailed(bytes32("Cashier_TransferFailed"));
    }
}
```

&#x20;  &#x20;

&#x20;   **(3) Reason of USDC Escrow**

The table below provides a summary of the reasons for escrow or releasing **USDC** margin and their ASCII codes.

<table><thead><tr><th width="143.27264404296875" valign="top">Scenario</th><th width="176.0909423828125" valign="top">Brief Description</th><th valign="top">ASCII Code (Bytes32 in Hex)</th></tr></thead><tbody><tr><td valign="top">Deposit Buy Order Margin</td><td valign="top">CustodyValueOfBid</td><td valign="top">0x437573746f647956616c75654f66426964000000000000000000000000000000</td></tr><tr><td valign="top">Release Margin to Company</td><td valign="top">CloseInitOfferAgainstBid</td><td valign="top">0x436c6f7365496e69744f66666572416761696e73744269640000000000000000</td></tr><tr><td valign="top">Release Margin to Seller</td><td valign="top">CloseOfferAgainstBid</td><td valign="top">0x436c6f73654f66666572416761696e7374426964000000000000000000000000</td></tr><tr><td valign="top">Refund Buy Order Margin</td><td valign="top">RefundValueOfBidOrder</td><td valign="top">0x526566756e6456616c75654f664269644f726465720000000000000000000000</td></tr></tbody></table>



</details>

### Source Codes

#### [RegCenter](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/center/RegCenter.sol)  |  [GeneralKeeper](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/GeneralKeeper.sol)  |  [Cashier](https://github.com/paul-lee-attorney/comboox/blob/master/contracts/comps/books/cashier/Cashier.sol)&#x20;
