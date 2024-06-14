# ⚔️ Steps to deploy a DAO on Q

## Abbreviations

| DAO | Decentralized autonomous organization |
| --- | ------------------------------------- |
| EP  | Expert panel                          |

## Goal

The system is designed to provide the ability to create a customized DAO on the Q blockchain with distinct roles and responsibilities.

## Audience&#x20;

The Q blockchain platform allows non-technical users to establish their own Decentralized Autonomous Organization (DAO). Anyone, regardless of their technical expertise, can participate in creating and managing a DAO. They can create a new ERC20 or ERC721 token (with enumeration extension) or set up their own token, or use the native Q Token to then use it to manage DAO.

## System structure

### Roles

#### DAO creator

The person or entity who has been granted the DAO creator role.&#x20;

During Smart Contract deployment, this account creates new Expert Panels and can add additional Expert Panels later if it has not revoked this role previously.&#x20;

In addition, this account can only set up veto groups for the DAO once. After that, they can only be changed/extended as part of the Governance process.&#x20;

The creator also has all the rights of a regular user.

#### DAO Member

A general DAO member is determined by depositing a DAO token or native Q in the DAO repository. Then, they can participate in votes open to all DAO members.

#### Expert

General DAO member with extended functions and responsibilities (e.g., the power to set certain parameters). They can vote on closed proposals for Experts only.&#x20;

There can be more than one Expert Group. Also, it is possible to be an Expert in multiple Expert Panels.&#x20;

Experts are selected or excluded by voting, in which all DAO token holders can participate.

#### Guardian

A group of DAO members who can veto selected voting results and thus ensure compliance with the DAO Constitution.&#x20;

The Guardian role can be assigned to Expert Panels.

It is possible to have different Guardians for different proposals.

### Basic Flows

**Note:** The functionality is available on the testnet and mainnet, but for each DAO network, you must create and configure your DAO separately.

{% content-ref url="dao-creation.md" %}
[dao-creation.md](dao-creation.md)
{% endcontent-ref %}

{% content-ref url="governance/" %}
[governance](governance/)
{% endcontent-ref %}
