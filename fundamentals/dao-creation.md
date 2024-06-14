---
description: Step by step documentation for deploying DAO on Q.
---

# 🏹 DAO Creation

{% embed url="https://factory.q-dao.tools/" %}
Tool to create a decentralized organization in a few clicks
{% endembed %}

To directly navigate to the front end for creating a DAO, you could use the link above.&#x20;

The DAO Creation process consists of 8 steps, where you will configure the base parts of the system:&#x20;

* Define the name and purpose of your DAO
* Use existing tokens or create a new one for your DAO (could be either ERC20/Native token or ERC721 with an enumeration extension or Consensual Soulbound Token/[ERC5484](https://eips.ethereum.org/EIPS/eip-5484))&#x20;
* Set up the necessary number of Expert Panels (maximum number is ten)&#x20;
* Decide which votings required for the system, and configure veto groups for them

In the end, you will need to confirm a few transactions: 2 are mandatory, where one is for main DAO contracts deployment and another for veto configuration. \
Additional transactions could be for Token (ERC20/ERC721/ERC5484) deployment and one transaction per Expert Panel.&#x20;

In the end, you will still have the DAO Creator role, you could revoke it with the SDK or leave it for future use. With it, you will be able to create an additional Exprt Panel up to the limit, which is 10 by default.&#x20;

The maximin panels per DAO limit could be changed by constitutional voting.&#x20;

Currently, there is no DAO constitution, will be able soon.

### **First step**

Now, let me explain how to create a DAO.&#x20;

First, you need to find the DAO creation button on the "DAO Factory" homepage. Anyone can use this button to make a new DAO.

When you click on it, you'll be asked to come up with a DAO Name and purpose. Name it is basically the name of your DAO, while the purpose will define what the DAO is all about. To give you an idea, here's the Preamble of the Q Constitution:

(A) Q is an open-source platform, not tied to any specific country, company, or organization.&#x20;

(B) Q's purpose is to serve humanity, and it'll continue to develop with that goal in mind.&#x20;

(C) All of us involved with Q, including Q Token Holders, Validator Nodes, Validator Node Candidates, Root Nodes, Q Nodes, and Q ID Holders (collectively known as "Q Stakeholders") voluntarily take part in Q and agree to this constitution (referred to as the "Q Constitution").

Just remember, whatever you write for the DAO Purpose will be included in the constitution that gets generated (will be able soon) when you create the DAO.

### Second step

Alright, let's break down the second step of creating a DAO for you. In this step, you'll decide how membership for the DAO will be determined. Here are the options you can choose from:

1. All Q Token Holders (native token of the Q Blockchain)
2. Use existing tokens (you'll need to provide the address of the token that will represent this DAO)
3. Create a new ERC20 token
4. Create a new ERC721 token
5. Create a new [ERC5484](https://eips.ethereum.org/EIPS/eip-5484) token

Keep in mind that only the holders of the selected token will be able to vote within the DAO. If you decide to create a new ERC20/ERC721/ERC5484 token, you'll have to fill in some fields. Some common fields are:

* Name and Symbol: These are self-explanatory.
* Total Supply Capacity: This is the maximum number of tokens that can be minted (an unchangeable parameter). For ERC20 tokens, this number will be multiplied by the `decimals` field.

Both types of tokens also have a Contract URI field, which is **optional** and can be used to provide token metadata.

For ERC20 tokens, there's a unique field called 'decimals,' which is similar to 'wei' in Ethereum. For example, if `decimals` is set to 2, then 200 represents 2 tokens, and 1 is the smallest part. The default value is 18, just like Ethereum.

For ERC721/ERC5484 tokens, there's a unique field called 'base URI,' which is the first part of the URI for all NFTs. For example, if you store all NFT metadata in IPFS, then "[https://ipfs.io/ipfs/](https://ipfs.io/ipfs/)" could be the base URI. When minting a token, you'd only need to enter the \<CID> of the NFT in the Token URI field. The baseURI field is **optional**.

The ERC5484 token is a Consensual Soulbound Token, with prohibited burning for the issuer and owner. It is non-transferable, and an account cannot have more than one token on its balance sheet.

The most important thing to remember is that the token you choose or create will be the main token for the DAO. If users want to participate in DAO voting, they must deposit the token into the DAO Vault.

### **Third step (Expert panels creation)**

Alright, let's go over the third step, which is about creating Expert Panels. To set up a new role (Expert Panel), you'll need to fill in these text fields:

1. Name
2. Purpose

You can create multiple Expert Panels (up to 10) by clicking the corresponding button. Make sure to be clear and specific when naming and describing the Expert Panels to ensure smooth DAO operations.

In the future, you'll be able to add addresses to a specific Expert Panel as well.&#x20;

Keep in mind that the text you input here will be included in the **DAO** **constitution** generated during the DAO creation process. However, smart contracts or other platform resources won't validate these fields.

Lastly, in the following steps, you'll have the option to select one or more Expert Panels as **Guardians** for different proposals.

### **Fourth step (Set governance structure)**

In the fourth step, you'll set up the governance structure of the DAO, deciding how it will function and who can vote on various matters. Here's what you can configure for all DAO participants using checkboxes:

1. Constitution Vote (Parameter Vote)
2. General Update Vote
3. EP Membership Vote(s)

Additionally, you can configure proposals for each Expert Panel (EP) created in the previous step. For each EP, you have these options:

1. EP General Update Vote
2. EP Parameter Vote

Here's a brief explanation of what these votes mean:

* General Update Vote: This is for raising general topics, which could be about anything. Through this voting, you can create additional voting situations, but currently, this can only be achieved through the SDK (check the advanced tab for more details).
* Constitution Vote (Parameter Vote): This is for changing parameters. Be cautious with this, as setting some parameters incorrectly (e.g., Voting Target) could break the DAO. More details on parameters can be found on the Governance page.
* Membership Vote: This is for becoming an expert on a specific panel, open to all DAO token holders. If chosen, you could access Parameter Votes and General Votes for experts and also have veto rights for some DAO votings, if it was set up.

Keep in mind that the number of distinct EP Membership Votes, EP General Update Votes, and EP Parameter Votes depend on the number of Expert Panels you created earlier.

For now, a 5% Quorum and a 50% Majority will be used as default parameters for all proposals. In the future, you'll be able to configure these settings during DAO creation. After the DAO is deployed, you can modify them through appropriate voting.

### **Fifth step (Create DAO treasury)**

In the fifth step, you'll create the DAO treasury, which will be responsible for collecting and redistributing the DAO's funds. You can use any address for the treasury, such as a centralized wallet, a multi-sig, or a smart contract.

Keep in mind that the treasury can be utilized if the DAO wants to use tokens or funds for a specific purpose.&#x20;

At the moment, there is **no technical implementation** for this step; as the DAO creator, you'll simply provide the treasury's address, and it will be stored with the constitutional parameters.&#x20;

### **Sixth step (**Set checks and balances**)**

In the sixth step, you'll set up checks and balances for your DAO by deciding which roles or Expert Panels (EPs) will have the power to veto proposal votes. If you haven't created any Expert Panels yet, you can create a new one that will act as a Guardian, responsible for vetoing proposals. This new "Guardian" Expert Panel won't have to vote on proposals themselves.

You have three options to choose from:

1. Select one of the previously created Expert Panels that will, by default, serve as a guardian for all proposals (except their own).
2. Create a new guardian role that will, by default, serve as a guardian for all proposals. To do this, fill in the text fields 'Name' and 'Purpose', just like in previous steps.
3. Don't select any default guardian, which means that proposals cannot be vetoed by default.

Remember that you can manually customize veto rights for each proposal in the next step. However, be aware that this can add complexity to your governance structure.

When creating a new role (Guardian) in this step, you'll fill in the same text fields as when creating Expert Panels. The information you provide here will be included in the DAO constitution, but smart contracts or other platform resources won't validate it.

### **Seventh step (**Customize the veto for some proposals**)**

In the seventh step, you'll have the chance to customize veto options for specific proposals. You can manually change veto rights for selected proposals from the default guardians to another Expert Panel. Various types of voting available for all DAO participants can be vetoed, such as Constitution Vote, General Update Vote, and EP Membership Votes.&#x20;

You can choose from options like any EP and the Guardian EP created in the previous step.

In the upcoming updates, you will be able to select from Q expert panels, such as Q Fees & Incentives Membership Panel, Q DeFi (Decentralized Finance) Membership Panel, and Q Root Node Selection Expert Panel.&#x20;

Simply put, this step lets you fine-tune the veto rights for different proposals by choosing the appropriate Expert Panel to oversee them, ensuring a balanced governance system for your DAO.

### **Eighth step (**Confirmation**)**

In the final step of the DAO setup (Eighth Step), you can check the information about your future DAO and, if necessary, modify it.&#x20;

In future, you will receive your constitution based on the rules you've chosen throughout the process. While the constitution can be stored locally, on IPFS, or in another location (this feature is coming soon), its hash will be uploaded to the contract.&#x20;

The constitution will be in the form of an ASCII doc but has yet to be created (also coming soon).

To summarize the entire process, you went through eight steps to set up your DAO, including creating Expert Panels, setting the governance structure, creating a treasury, establishing checks and balances, customizing veto rights, and generating the constitution. By following these steps, you've successfully laid the foundation for a well-organized and functional DAO.

<mark style="color:orange;">**Thanks for creating a DAO with Q!**</mark>

