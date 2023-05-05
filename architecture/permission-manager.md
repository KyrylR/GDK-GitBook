# 📕 Permission Manager

In the context of permissions within a DAO, it is essential to understand that all permissions are stored in a single contract (PermissionManager.sol). This means that in order to access any module in the system (e.g., to vote, veto, or make a proposal), you must have the appropriate permission to do so.

The primary function of the PermissionManager contract is to manage permissions and roles within a DAO. It enables the creation, modification, and deletion of roles and permissions, as well as the assignment of these roles to specific addresses or groups of addresses.

Permission Manager is based on[ the RBACGroupable module](https://github.com/dl-solidity-library/dev-modules/blob/master/contracts/access-control/extensions/RBACGroupable.sol), which in turn is based on [the RBAC module](https://github.com/dl-solidity-library/dev-modules/blob/master/contracts/access-control/RBAC.sol).

### Role-Based Access Control (RBAC) Module

The RBAC module is an advanced system that manages role assignments for large systems. It allows for the declaration of specific permissions for specific resources (contracts) and the aggregation of these permissions into roles for subsequent user assignment.

Each user can have multiple roles, and each role can manage multiple resources. Additionally, each resource can have a set of permissions (e.g., CREATE, DELETE) that are only valid for that specific resource.

In the GDK system, the following definition applies:

* **All** contracts in the system are **resources**.
* Over each **resource,** you can perform **actions**.

The RBAC model also supports anti-permissions, which can be granted to users to restrict their access level. A special wildcard symbol "\*" represents "everything" and can be applied to both resources and permissions.

[The RBACGroupable extension](https://github.com/dl-solidity-library/dev-modules/blob/master/contracts/access-control/extensions/RBACGroupable.sol) provides the functionality to create a group to which roles can be granted. If a user is included in a group, they automatically inherit the same roles as the group.

### Example

Let's examine the proposal creation flow as an example.

To create a proposal, a user must call the following function:

_createProposal(string situation, string remark, bytes callData) onlyCreateVotingPermission_

In this example, let's go over the checks that a user must pass in order to create a proposal.

<details>

<summary>First check: <code>onlyCreateVotingPermission</code></summary>

This first one will be `onlyCreateVotingPermission` modifier. A similar _modifier_ has every function in the system, and a pattern for those modifiers is only\<Action>Permission, where _Action_ could be any verb, for example: Execute, Create, Delete, VoteFor (to be more accurate, it is a shortcut for the _Vote For some purpose_), Veto, etc.

Let’s come back to the `onlyCreateVotingPermission`modifier. Inside this modifier, we will find a call to the internal function in which the following `require` stand:

```
...
modifier onlyCreateVotingPermission() {
  _requireVotingPermission(CREATE_VOTING_PERMISSION);
  _;
}
....
function _requireVotingPermission(string memory permission_) internal view {
  require(
     permissionManager.hasPermission(msg.sender, DAO_VOTING_RESOURCE, permission_),
     "[QGDK-018014]-The sender is not allowed to perform the action, access denied."
  );
}
...
```

We could decode the `require` above like that: Ask permission manager if the user (`msg.sender`) has permission to perform some action (`permission_`, in this case, it is `CREATE_VOTING_PERMISSION`) on the resource (`DAO_VOTING_RESOURCE`).

As a result, to pass the first check, the user must have `CREATE_VOTING_PERMISSION` for `DAO_VOTING_RESOURCE`!

_The user must deposit some tokens into the DAOVault contract to get this permission._

</details>

<details>

<summary>Second check: validate voting situation existence</summary>

After the user gets permission to create votings, the next check will be:

```
require(
  _votingSituations.contains(situation_),
  "[QGDK-018002]-The voting situation does not exist, impossible to create a proposal."
);
```

Currently, every Vote works through the concept of the situation.

Remind string situation passed to the `createProposal(...)` function, and it is just a pointer to the DAOParameter storage, which helps retrieve all necessary information to create voting.\
The following structure could represent this information:

```
struct DAOVotingValues {
  uint256 votingPeriod;
  uint256 vetoPeriod;
  uint256 proposalExecutionPeriod;
  uint256 requiredQuorum;
  uint256 requiredVetoQuorum;
  uint256 votingType;
  string votingTarget;
  uint256 votingMinAmount;
}
```

Inside this _structure,_ the most important field is string `votingTarget`, with which the contract can define which target it should interact.

_The user must choose an existing voting situation to pass the checkpoint._

</details>

<details>

<summary>Third check: validate for General Voting</summary>

The next _require_ is used to check that user will not break anything by passing an empty callData argument and will choose as a target, not a voting contract.

```
require(
  callData_.length > 0 || newProposal.target == address(this),
  "[QGDK-018003]-The general voting must be called on the Voting contract."
);
```

Let’s quickly switch to the central part of the `executeProposal` function. To be more accurate, we will cover the second line of code for now**.**

```
...
if (proposal_.callData.length > 0) {
  (bool success_, ) = address(proposal_.target).call(proposal_.callData);
  require(success_, "[QGDK-018008]-The proposal execution failed.");
}
...
```

This if statement checks: if the passed callData to the `createProposal(...)` function is more than 0. It means that the user wanted to change the state of some contract (i.e. change parameter, add member, update contract, add veto group, etc.)

But if he has passed empty `callData`, he wanted to create a General Update Proposal to raise some topic or something similar.

So as not to make the user confused, he is only able to create the General Update Proposal if he has passed empty `callData` and as a target specified DAOVoting contract.

_The user must pass not empty callData if he wants to change something at the target contract; he could choose any contract that implements the IDAOResource interface._

_Or if he wants to raise some topic, he will need to choose a situation where the target is the DAOVoting contract and pass an empty callData._

</details>

<details>

<summary>Fourth check: _requireResourcePermission</summary>



The next step is to check if the user has permission to create voting with the purpose of changing anything in the target contract.

```
...
_requireResourcePermission(newProposal.target, VOTE_FOR_PERMISSION);
...
function _requireResourcePermission(
  address targetContract_,
  string memory permission_
) internal view {
  require(
     IDAOResource(targetContract_).checkPermission(msg.sender, permission_),
     "[QGDK-018015]-The sender is not allowed to start the vote on the target, access denied."
  );
}  
```

The target **must** implement the `IDAOResource` interface to be chosen as a voting target!

Currently, contracts that implement this interface are:

DAOParameterStorage, DAOMemberStorage, GeneralDAOVoting, ExpertsDAOVoting, DAORegistry, PermissionManager.

Let’s iterate over each one and see which things could be changed through voting!

DAORegistry and PermissionManager are special contracts, and only through the DAO's main voting can they be configured.

Also, for each Expert Panel, 3 contracts are deployed: DAOParameterStorage, DAOMemberStorage, and ExpertsDAOVoting, so if the user wants to change some parameter in the Expert Panel, he must create voting through the appropriate ExpertsDAOVoting contract that is related to this Expert Panel.

In the DAOParameterStorage contract, they will be able to call the following protected methods:

* setDAOParameter(...) / setDAOParameters(...)
* changeDAOParameter(...) / changeDAOParameters(...)
* removeDAOParameter(...) / removeDAOParameters(...)

In the DAOMemberStorage contract:

* addMember(...) / addMembers(...)
* removeMember(...) / removeMembers(...)

In the ExpertsDAOVoting or GeneralDAOVoting contracts:

* createDAOVotingSituation
* removeVotingSituation

In the DAORegistry contract (only through main DAO voting could it be called)

* addPanel (If the user adds a name, nothing will be deployed in the background).
* removePanel (If the user first deletes the panel and then calls the deployDAOPanel function from MasterDAOFactory, the old contract addresses from the last panel will be overwritten in the DAORegistry with the new contract addresses, which means that it will be almost impossible to restore the old contracts.)&#x20;

<!---->

* upgradeContract / upgradeContractAndCall
* addContract / addProxyContract / justAddProxyContract

In the PermissionManager contract (only through main DAO voting could it be called)

* addVetoGroup / addVetoGroups
* linkStorageToVetoGroup
* addVetoGroupMember
* removeVetoGroupMember
* **confExternalModule**

_To create a proposal, the user must have VOTE\_FOR\_PERMISSION permission to access the resource of one of the above contracts._

</details>

<details>

<summary>Fifth check: validate user voting power</summary>

The next check is whether the user has enough tokens to create a proposal.

```
require(
  daoVault.getUserVotingPower(msg.sender, votingToken) >=
    daoParameterStorage
      .getDAOParameter(getVotingKey(situation_, votingKeys.votingMinAmountKey))
      .decodeUint256(),
  "[QGDK-018004]-The user voting power is too low to create a proposal."
);
```

The `votingMinAmount` could be changed through the Governance process or initialized during the DAO deployment.

_The user must deposit enough tokens to the DAOVault contract to pass this checkpoint._

</details>

<details>

<summary>Sixth check: validate if the Proposal only for Experts</summary>

The last check is created for Expert Proposals:

```
...
if (newProposal.params.votingType != VotingType.NON_RESTRICTED) {
   _checkRestriction();
}
...
// ExpertsDAOVoting.sol
function _checkRestriction(VotingType votingType_) internal view override {
  require(
    permissionManager.hasPermission(msg.sender, DAO_VOTING_RESOURCE, EXPERT_PERMISSION),
    "[QGDK-017000]-Permission denied - only experts have access."
  );
}

// GeneralDAOVoting.sol
function _checkRestriction() internal view virtual {
  revert("[QGDK-018012]-The restricted voting is not supported.");
}
```

_The user must have the EXPERT\_PERMISSION in order to create a Restricted or Partially Restricted proposal._

_He can get these permissions if he is added to the DAOMemberStorage of Expert Panels as an expert (can only be done by the membership voting)._

</details>

