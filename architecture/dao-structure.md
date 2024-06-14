# 📑 DAO structure

The components below work together to create a decentralized governance system allowing transparent decision-making and resource management within the DAO.

The following contracts form the DAO:

**DAORegistry**: it is the contracts registry where all contracts (QRCs, Permission Manager proxy, Vault, etc.) related to the DAO are stored.

**PermissionManager**: every time a contract or user interacts with a DAO, their credentials will be checked through the PermissionManager contract.

**DAOVault**: implements functionality for depositing, locking and withdrawing tokens. The following standards are currently supported: ERC20, ERC721 and Native Token.

**Voting Factory and Registry**: contracts work together to deploy the DAOVoting contract. Currently is used only by the MasterDAOFactory contract.

The three contracts form the Expert Panel:

**DAOParameterStorage:** all parameters related to the DAO are stored in this contract.

There are two types of parameter storage for expert panels:&#x20;

* Configuration Parameters Storage
* Regular Parameters Storage&#x20;

The configuration parameter storage stores all parameters related to the voting process (i.e. voting period, veto period, etc.).&#x20;

The regular parameter storage contains all parameters related to the area of expertise of the experts

**DAOMemberStorage**: the experts of the panel listed in this contract.

**DAOVoting**: through this contract, you could create proposals to add members, change parameters, etc.

Through Main DAO Parameters, the user could define the limit of the Expert Panels in the DAO.

### Flows

Here are some flow charts that can be created to describe the processes within the DAO:

<figure><img src="../.gitbook/assets/Proposal Creation Flow.drawio.png" alt=""><figcaption><p><strong>Proposal Creation Flow</strong></p></figcaption></figure>

**Proposal Creation Flow**: This flow chart would depict the steps involved in creating a proposal, including permission checks, voting situation selection, target contract selection, and resource permission checks

As you can notice from the flow, the PermissionManager contract is a crucial part of the system. Currently, it is impossible to interact with the Permission Manager contract directly.\
The user could only obtain permissions by interaction with wrapper contracts (i.e. DAOVault, DAOMemebrStorage, DAOVoting).
