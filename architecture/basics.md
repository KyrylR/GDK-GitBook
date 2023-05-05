---
description: >-
  In this section, we will look at the features of the GDK core and how all of
  the above has been achieved.
---

# 📃 Basics

## Main System Paradigm

For this journey, you should remember the following:

> **All** contracts in the system are **resources**.

> Over each **resource** you can perform **actions**.

And the binding glue between contracts and users is roles.

### Role Model

The role is built from resources, and each resource has an array of actions. Resources and actions are divided into two types - what the role allows to do and what it disallows.

Each contract has its own name. And each contract's method has its own action category.

The action is prohibited by default if neither permission nor prohibition is defined for a certain resource. It's also important to note that disallow takes precedence over allow.&#x20;

The action will be prohibited if the same resource and action are specified in allow and disallow.

For example, to call the `voteFor` method in the **General DAO Voting** **contract**, you need at least the resource: _general voting_ and action: _vote_.

The role verification process looks like this:

1. We look in disallow if the resource and action are in it - the operation is rejected.
2. If it is not found, see if there are \*. If there is - the operation is rejected.
3. If it is not found, the contract looks in allow. If the resource and action are not there, we check the \*. If yes, allow.

Where the \`**\*\`** symbol represents all resources or all permissions.
