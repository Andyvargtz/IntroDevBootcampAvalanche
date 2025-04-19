---
icon: square-small
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Decentralized Storage for NFTs

In the world of NFTs, each token typically has unique information, such as images, names, or descriptions, that form its **metadata**. However, this information is not stored directly on the blockchain, as storing large amounts of data on the chain can be expensive and impractical. Instead, **decentralized storage** and a **URI** (Uniform Resource Identifier) are used to manage this data efficiently.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### **What is IPFS?**

**IPFS** (InterPlanetary File System) is a decentralized storage system that allows files to be stored and shared securely without depending on a central server. Instead of storing files in a specific location (like a server), IPFS stores data in a network of distributed nodes (computers). This means that:

* Files uploaded to IPFS receive a **CID** (Content Identifier), which is a unique identifier based on the file's content.
* This **CID** serves as a permanent address for the file, even if a copy of the file is lost on one node, IPFS will find another copy in the network.
* IPFS ensures that data is immutable: if the file changes, its CID also changes.

In the case of NFTs, IPFS is used to store token images and metadata. Thus, each NFT can point to a specific file in IPFS that contains its unique information.

### **What is Base URI?**

The **Base URI** is a base address used in the ERC721 contract to build the link to each NFT's metadata. Instead of storing a complete link for each token, a general **Base URI** is defined, and then each token uses its `tokenId` to access its specific data.

For example, if we set the Base URI as:

```arduino
ipfs://QmXyZ.../collection/
```

For the token with `tokenId` 1, the complete link to its metadata will be:

```arduino
ipfs://QmXyZ.../collection/1
```

This approach allows efficient management of metadata links, making all NFTs in a collection share the same base URI but have unique addresses based on their `tokenId`.
