---
description: Here you will find basic information to dive deep into DAO Governance process.
---

# 🏛 Governance

When it comes to governing a DAO, the process can vary from one system to another.&#x20;

At its core, Q DAO governance is layered, which means groups of people have special rights or privileges. For instance, in the DAO created by GDK, there are Expert Panels and Guardian Panels.

Expert Panels consist of individuals with extensive knowledge in specific areas, such as DeFi, Bridge, Oracles, or any other field in the web3 or web2 domains. The community chooses these experts to be responsible for certain aspects of the DAO. They can raise topics for discussion and vote on new parameters.

Guardian Panels, on the other hand, can veto certain proposals. Any Expert Panel can also act as a Guardian if it was set up that way beforehand. These guardians are trusted members of the DAO community, and they serve as a final line of defence before the community accepts a proposal at large. As the name suggests, they protect the community from making poor decisions.

For example, let's say there's a proposal to invest a significant portion of the DAO's funds into a high-risk project. The Expert Panel specialized in DeFi might evaluate the proposal and determine it's too risky. They can then raise their concerns and vote against it. If the proposal still gains traction, the Guardian Panel can step in and veto the proposal to prevent the community from making a potentially harmful decision.

## Examining Key DAO Aspects

### Parameters

**Updatable Functionality and Parameters**

All parameters impacting the governance and process can be updated, including the voting period, veto period, minimum tokens that a user needs to deposit to the DAO Vault, whether the constitution has a treasury, etc.&#x20;

Essentially, all parameters in the DAO Parameters tab can be changed.&#x20;

As a result, functionality could also be changed, such as if some contracts were upgraded or added to the DAO Registry. Voting base parameters, change will naturally impact the voting and veto process (governance).

**Different Rules for Updating Functionality and Parameters**

Not all parameters have the same rules for updating. Experts can only change some parameters through restricted voting, while the community can change others through constitutional voting (non-restricted voting).&#x20;

In the latter case, experts can create a proposal, but the entire community can participate in the vote. This is called partially restricted voting. The last option can be configured manually.&#x20;

To better understand how this works, refer to the Voting Process subpage.

**Major and Minor Updates**

The governance power is distributed between the Expert Panel and the community and may vary from DAO to DAO.&#x20;

By default, the community makes major changes to the DAO governance process and updates and can be protected by Guardian Panels.&#x20;

The experts handle changes at the level of Expert Panels (EP General Vote or EP Parameter Vote) by default.

**Off-Chain and On-Chain Updates**

Everything is handled on-chain, but if a DAO wants, they could implement off-chain updates. However, the core concept is that everything is handled on-chain.

**Changing Governance Rules**

Governance rules can be changed through the governance process.&#x20;

For example, experts could decide to migrate from restricted to non-restricted voting, or the community could modify voting and veto periods to be shorter or longer.



### Governance Participation Assets

#### Single Fungible Token

At the basic level, a single fungible token is used for all decisions, such as an ERC20 or an ERC721 with the enumeration extension.&#x20;

The enumeration extension is required for ERC721 tokens to count the total quorum.&#x20;

On an advanced level, the DAO creator could set up different tokens for different expert panels, but the DAO Dashboard does not currently handle this case.

#### Multiple Fungible Tokens and Ratios

Only one token can be used as voting power for one Expert Panel.&#x20;

Therefore, it is impossible to have voted in the Expert Panel and vote with different tokens, and no ratio is involved. Tokens are considered as voting power only, and if deposited, they allow participation in the voting.&#x20;

To become an expert, a user must start a membership vote, put themselves up as a candidate, and have the community approve their candidacy.

#### Non-Transferable Fungible Tokens

By default, non-transferable fungible tokens are not used for voting.&#x20;

However, the DAO creator could set up a fungible but non-transferable token for voting if they create such a contract, create a DAO, and choose an existing token as the DAO Token.

#### Non-Fungible Tokens and Voting Rights

NFTs can be chosen as DAO Tokens, but their usage is very simple. Each NFT equates to one vote, and even if a user has more than one NFT, it still counts as a single vote.&#x20;

As with fungible tokens, users must deposit their NFTs to the DAO Vault to be able to vote.

#### Delegation of Assets

There is no default delegation process in the basic DAO structure.



### Proposal Creation Process

#### Eligibility for Making Proposals

The eligibility to make proposals depends on the voting type, which can be checked in the DAO parameters tab. There are three types:

1. Non-restricted voting (Type 0): Anyone can create a proposal, and everyone will vote for or against it. Examples include Constitution Votes or Membership Votes in any Expert Panel by default.
2. Restricted voting (Type 1): Only certain Experts can create proposals, and only other experts can vote for or against them. An example is the Parameter Vote in any Expert Panel by default (although this could change over time).
3. Partially restricted voting (Type 2): Only experts of a certain panel can create voting, but all DAO Token Holders can participate in it.

#### Token Requirements for Proposals

On a basic level, users should have a certain amount of DAO Tokens deposited in the DAO Vault to participate in the governance process. This requirement applies to both regular users and Experts. The minimum amount needed for the deposit is specified in the DAO parameters.

On an advance, it is the same, but the user must deposit the required token for a certain Expert Panel if it was configured.

#### Staking and Locking Tokens

By default, there is no stake in the system. However, tokens are locked when users vote on proposals. Locked tokens are considered as voting power in the system, so voting power is based on locked tokens plus tokens that users can withdraw from the vault.



### System Improvement Process

#### Improvement Scope

If the DAO community wants to extend the system functionality, they can integrate it with a new contract.&#x20;

Anyone can propose improvements to the DAO through the voting process, similar to a parameter vote. The process is described in the Advanced section.&#x20;

To add the contract to the DAO Registry, only one community voting is needed. An additional proposal should be created if the contract needs to be integrated with the Permission Manager.

#### Improvement Validation and Decentralization

The entire community should validate the contract because it could bring significant damage to the DAO system, especially if the Permission Manager is involved. As an additional measure, the Guardian Panel can also validate the setup if it is configured.&#x20;

The improvement process is similar to the Ethereum Improvement Proposal (EIP) system, with no punishment considered. Since everything is done on-chain, the process is entirely decentralized.



### Monetization Process

At this stage, the system does not have a built-in monetization or incentive structure for proposal creation or implementation. The current focus is on providing a solid governance foundation for DAOs, allowing them to build additional systems and features on top of this base as needed.

As such, the following questions related to monetization, incentives, or fees are not applicable to the current scope of the system:

* The decision-making process for monetizing incentives for proposals
* Rules or criteria for monetizing proposals
* Penalties for specific actions
* Payment stages for proposal creators
* Timeframes for payments after system updates
* Appeal procedures for payments

The system can be further developed or customized by the community to address these aspects in the future if desired by DAO.



### DAO Environment and Chain Compatibility

The current DAO implementation is designed for a single chain and is deployed on the chain selected by the user, which could be either a testnet or mainnet. The system does not support multi-chain environments or different types of chains (such as Cosmos-based) at this stage. As a result, the following aspects related to multi-chain compatibility are not applicable:

* Support for different types of chains (Cosmos-based, etc.)
* Different rules or governance structures on different chains
* Variation in decision-making weight across chains
* DAO token transfers between chains, but the Q Token bridge could be used to transfer DAO Token to Ethereum.
* Cross-chain transfers within the DAO Governance process

Future development and customization by the community can explore and address these aspects if needed, potentially extending the system's compatibility with multi-chain environments.
