# 🗂️ Structure of the DAO Factory contracts

Four contracts form the **Main DAO Factory** system:

1. Master Access Management
2. Master Contracts Registry
3. Master DAO Factory
4. Master DAO Registry\


<figure><img src="../.gitbook/assets/Master DAO Dactory.drawio.png" alt=""><figcaption><p>Master DAO Factory Stucture</p></figcaption></figure>

1. The MasterAccessManagement contract controls permissions for the MasterDAOFactory and MasterDAORegistry. For example, we give DAO creator CONFIGURE\_DAO\_PERMISSION permission for the MasterDAOFactory resource, allowing them to deploy new DAO Panels or configure the veto groups.
2. The MasterContractsRegistry contract serves as a central registry for the addresses of the Main DAO Factory contracts, such as MasterDAOFactory and MasterDAORegistry.
3. The MasterDAOFactory contract is responsible for deploying DAOs and DAO modules.\
   It is the main module of the system. It deploys and initializes the DAO. Also, through this contract, new DAO Expert panels could be deployed and veto groups configured.
4. The MasterDAORegistry contract stores the base DAO contract implementations.\
   All implementations for DAO deployment are stored in this contract. During the deployment of the DAO, each time to Deploy a new contract, the \`MasterDAOFactory\` will ask for the implementation address from this contract by its name.

Below are the flows for the initial deployment and interactions with **Main DAO Factory.**

<figure><img src="../.gitbook/assets/Initial stage.drawio.png" alt=""><figcaption></figcaption></figure>

The MasterDAOFactory contract is responsible for deploying and initializing DAO and their associated modules. It is a central part of the system and can also be used to deploy new DAO expert panels.

### Main ideas

1. Deploying and initializing DAOs and their modules.
2. Deploying new DAO expert panels.
3. Providing methods to deploy and configure DAO components, such as token factories, voting factories, and member storage. Currently, all of them are private.
4. Interacting with permission management to ensure proper access control.

### How it works

1. The deployDAO function deploys a new DAO by creating a DAORegistry instance and initializing it with the necessary modules and configurations. It deploys the DAO vault, token factory, voting factory, and main DAO expert panel.
2. The deployDAOPanel function deploys a new DAO panel consisting of DAOParameterStorage, DAOMemberStorage, and a voting contract. It adds the panel to the DAORegistry, initializes the modules, and grants necessary roles and permissions.
3. The configureVetoGroups function configures veto groups for a DAO, ensuring that only those with the proper permission can have veto power on defined types of voting.

It is not recommended to interact directly with this contract. Instead, developers should use the provided SDK to interact with the system.

Here are the flow charts for better understanding.

<figure><img src="../.gitbook/assets/Calls to Master DAO Factory.drawio.png" alt=""><figcaption></figcaption></figure>

\


\


\
