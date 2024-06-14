---
description: This page describes how the DAO guard mechanism works.
---

# 🛡️ Veto process

The veto process plays a vital role in DAO governance, as it serves as a last resort to stop a proposal that may not align with the DAO's constitution. Vetoes are available exclusively to Guardians and External Guardians, as determined during the DAO setup.

The primary purpose of the veto process is to ensure that all proposals adhere to the DAO's constitution and principles. It provides a safeguard against potentially harmful or misaligned decisions by allowing Guardians and External Guardians to halt the proposal's execution before the voting results are implemented.

When a proposal is up for a vote, Guardians and External Guardians can evaluate its merits and alignment with the DAO's constitution. If they determine that the proposal is not in the best interest of the DAO or its members, they can exercise their veto power to stop it from being implemented.

The veto process is a critical tool to maintain the integrity of the DAO and ensure that all decisions align with the organization's values and goals. By granting veto power to Guardians and External Guardians, the DAO can prevent potentially harmful proposals from being executed, thereby protecting the best interests of its members.

### Veto Configuration

A veto can be configured for each contract within the DAO. Each contract in the DAO is considered a resource, and eligible users can veto proposals targeting specific contracts that implement the `IDAOResource` interface.

For example, the `GeneralDAOVoting.sol` the contract is represented by a Veto Group, which has the following structure:

```
struct VetoGroup {
    string name;
    address target;
    DAOMemberStorage linkedMemberStorage;
}
```

The Veto Group parameters are as follows:

* `name`: The name assigned to the veto group.
* `target`: The most important parameter in the structure, representing the contract on which users can create proposals (e.g., `GeneralDAOVoting.sol`).
* `linkedMemberStorage`: The address of the `DAOMemberStorag.sol` contract, representing members from a specific Expert Panel who also have veto power, along with users from the `members` list.

Eligible users who have veto power should be in the Member Storage of some Expert Panel. These users can veto proposals of a specific voting target, which should always be a contract that implements the `IDAOResource` interface.

The duration within which a decision can be vetoed is customizable from DAO to DAO, as determined by the `vetoPeriod` parameter that can be found in the DAO Parameters tab.

In summary, the veto process is an essential component of DAO governance that helps maintain the organization's integrity and adherence to its constitution. By granting veto power to Guardians and External Guardians, the DAO ensures that all proposals align with the organization's values and goals, safeguarding its members' best interests.

