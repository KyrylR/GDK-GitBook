---
description: Here I will describe how to integrate external contracts into the DAO
---

# ⚙️ External module integration

After establishing base governance, a DAO may want to expand its ecosystem by integrating additional modules, such as a DAO Bridge, Uniswap, a Treasury, or any other components that demand DAO governance influence. The DAO system includes an External Module integration mechanism to facilitate this growth.

### How it works

To add a contract to the DAO and enable the creation of votes with the new contract as the voting target (as well as vetoes on such votes), you need to create a contract (or modify an existing one) that implements the `IDAOResource` interface. This interface is necessary for DAO voting contracts to verify if a user has permission to create a proposal, vote, or veto. Of course, it is totally up to up to customize this logic and play around.

Once the contract is created (extended), you can add it to the DAO Registry through a proposal. However, it is essential to note that creating such a proposal through the front end is currently impossible, and you will need to use GDK SDK Tools (coming soon).

### Integrating with the Permission Manager Contract

You should also implement the interface if you want to integrate your contract with the Permission Manager contract. This interface is responsible for adding new permissions for resources to the existing roles within the DAO.

You can use the getters in the `Globals.sol` contract to obtain the name for a specific role in the DAO. Additionally, GDK contracts can be accessed through the NPM registry; refer to the Resources section for the link.

After that, you will need to create a proposal for integration with the permission manager; see GDK SDK Tools help or use the unit test in Resources.&#x20;

The community **must be fully involved** in the integration process because if a dangerous contract is integrated, it could easily **break Governance control**, **steal deposited funds**, etc.

In summary, expanding the DAO ecosystem with external modules allows for greater flexibility and functionality within the organization. By implementing the `IDAOResource` and `IDAOIntegration` interfaces, you can seamlessly integrate new components and ensure they operate under the DAO's governance system.

### Resources

{% embed url="https://gitlab.com/q-dev/q-gdk/gdk-contracts/-/blob/main/contracts/interfaces/IDAOResource.sol" %}
Interface for a contract that is a resource of a DAO.
{% endembed %}

{% embed url="https://gitlab.com/q-dev/q-gdk/gdk-contracts/-/blob/main/contracts/interfaces/IDAOIntegration.sol" %}
Interface for integratin an external module into DAO .
{% endembed %}

{% embed url="https://gitlab.com/q-dev/q-gdk/gdk-contracts/-/blob/main/contracts/mock/external-module/TreasuryMock.sol" %}
Example of contract for the integration
{% endembed %}

{% embed url="https://gitlab.com/q-dev/q-gdk/gdk-contracts/-/blob/main/test/voting/ExternalModuleIntegration.test.js" %}
Test example of External Module Integration
{% endembed %}

{% embed url="https://www.npmjs.com/package/@q-dev/gdk-contracts" %}
GDK contract in the NPM registry
{% endembed %}
