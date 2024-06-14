# 🔏 DAO Vault

The DAOVault contract is designed as an entry point into DAO governance.&#x20;

This contract is responsible for storing, tracking and locking DAO-related funds, including Q, ERC20 and ERC721 tokens. In addition, the user can authorize with ERC5484 tokens.

### How it works

The contract uses PermissionManager to define who has access to interact with this contract. It checks whether an account has specific permissions to access the DAO Vault storage resource.

So, to be able to update any parameter in this contract, the caller must have an _Update permission_ for the _DAOParameterStorage resource_.

Currently, only the voting contract has this permission. It is used to lock the user tokens for the voting period.

{% hint style="info" %}
The user could freely deposit and withdraw funds without needing specific permission.
{% endhint %}

Under the hood, it uses the TimeLocks library: ​[https://gitlab.com/q-dev/q-gdk/gdk-contracts/-/blob/main/contracts/libs/TimeLocks.sol](https://gitlab.com/q-dev/q-gdk/gdk-contracts/-/blob/main/contracts/libs/TimeLocks.sol).

Which is based on the PriorityQueue library ​[https://github.com/dl-solidity-library/dev-modules/blob/master/contracts/libs/data-structures/PriorityQueue.sol](https://github.com/dl-solidity-library/dev-modules/blob/master/contracts/libs/data-structures/PriorityQueue.sol)

Where the priority is the amount (in the case of NFT/SBT, it is tokenId), and the End Lock time is the value.

With this approach, the biggest locked amount always will be at the top of the list (in case of ERC20 and Native tokens).

### Limitations and Considerations

1. Upgradability: This contract is upgradeable. The process of upgrading the default DAO modules will be described separately.
2. Token Compatibility: The DAOVault contract is designed to support ERC20, ERC721, ERC5484 and Native tokens. Additional modifications or extensions may be necessary if a DAO requires support for other token standards or non-token assets.

\
