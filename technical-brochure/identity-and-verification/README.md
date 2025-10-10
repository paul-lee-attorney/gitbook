# 👨‍🚀 Identity and Verification

The smooth operation of the **system** and the realization of functions, depend on the authority control and the routing control of the writing instructions. In other words, for the calling instructions ("**writing instructions**") which can change the state of each smart contract, it is necessary to review and verify the identity and authority of the account that issued the instructions, and at the same time, it is necessary to strict control the target contract address and API referred by the writing instructions. When the writing instructions are strictly controls from the "receiving” and “sending" direction, the information of the whole system can be updated as the established commercial and legal logic.

The writing instructions in the system can be divided into three categories:

1. **System Configuration**: the drafting and system configuration actions triggered by external accounts, and will not directly lead to legal consequences;
2. **Legal Behavior**: the share transactions and corporate governance activities triggered by external accounts, and will not lead to direct legal consequences; and
3. **Algorithmic Control**: the actions triggered by the first two types of writing instructions, in which the **bookkeeper contract** may issue the writing instructions in orderly manner to change the **Register Contract**, **shareholders agreement**, **investment agreement**, and other smart contracts.

For the above three types of **writing instructions**, the system adopts three verification methods to control the access varying from the behaviors and scope of influence.

{% content-ref url="role-and-rolesrepo.md" %}
[role-and-rolesrepo.md](role-and-rolesrepo.md)
{% endcontent-ref %}

{% content-ref url="access-control-contract.md" %}
[access-control-contract.md](access-control-contract.md)
{% endcontent-ref %}

{% content-ref url="user-and-usersrepo.md" %}
[user-and-usersrepo.md](user-and-usersrepo.md)
{% endcontent-ref %}



