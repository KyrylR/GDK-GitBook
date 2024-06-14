# 🗃️ DAO Storages of parameters and members

Managing the DAO parameters and members is done by the following contracts DAOParameterStorage and DAOMemberStorage

During the deployment of the Expert Panel

## DAO Parameter Storage

The DAOParameterStorage contract is designed to store and manage parameters for a DAO panel. This contract is responsible for storing parameters related to various resources, such as voting situations with their parameters (voting type, voting duration, etc.).

All parameters related to the Expert Panel should be stored in the appropriate DAOParameterStorage.

### How it works

1. Initialization: The contract is initialized with a resource identifier. In this case, it is a _panel name_.\
   So we could quickly identify to which panel the DAOParameterStorage contract belongs.\
   Also, this contract is AbstractDependant and follows [EIP-6224 standard](https://ethereum-magicians.org/t/eip-6224-contracts-dependencies-registry/12316), so the setDependencies function is called by the MasterDAOFactory to inject the necessary dependencies, such as the DAORegistry and the PermissionManager.
2. Permission Management: The contract uses PermissionManager to define who has access to interact with this contract. It checks whether an account has specific permissions to access the DAO Parameter storage resource.\
   So, to be able to create/update/delete any parameter in this contract, the caller must have one of the following permissions for the DAOParameterStorage resource:\
   &#x20;  \- Create permission\
   &#x20;  \- Update permission\
   &#x20;  \- Delete permission\
   \
   Currently, only the voting contract has such permissions.\

3. Parameter Management: The contract allows **setting**, **changing**, or **removing** single or multiple DAO parameters.

The following structures could represent DAO Parameter:

```
enum ParameterType {
    NONE,
    ADDRESS,
    UINT,
    STRING,
    BYTES,
    BOOL
}

struct Parameter {
    string name;
    bytes value;
    ParameterType solidityType;
}
```

So everything is stored in bytes format and _encoded/decoded_ when needed through the ParameterCodec library: [https://gitlab.com/q-dev/q-gdk/gdk-contracts/-/blob/main/contracts/libs/Parameters.sol#L23](https://gitlab.com/q-dev/q-gdk/gdk-contracts/-/blob/main/contracts/libs/Parameters.sol#L23).

### Limitations and Considerations

1. Upgradability: This contract is upgradeable. The process of upgrading the default DAO modules will be described separately.
