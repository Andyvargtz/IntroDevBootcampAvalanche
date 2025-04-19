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

# Introduction to Cryptography

Cryptography is another fundamental pillar in the functioning of blockchains. Without it, it would be practically impossible to guarantee the security and integrity of transactions and stored data. But how exactly does cryptography work in this context?

It all begins with **cryptographic hash functions**. These functions take an input of any size and produce a fixed-size output, known as a hash. The interesting thing is that if you change even a single character in the input, the resulting hash will be completely different. This ensures that any alteration in a block is easily detectable, as the block's hash would change and break the chain.

<figure><img src="../.gitbook/assets/Hhola (1).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/hola.png" alt="" width="563"><figcaption></figcaption></figure>

As you can observe, the hash changes completely even though we're only changing the uppercase "H" to lowercase. You can experiment with hashes on the following page:

{% embed url="https://10015.io/tools/sha256-encrypt-decrypt" %}

Additionally, each block in the blockchain contains the hash of the previous block, creating an immutable chain of linked blocks. If someone tried to modify a previous block, they would have to recalculate the hashes of all subsequent blocks, which is computationally infeasible in a large and distributed network.

Another essential component is the **public key and private key system**. Each user in the blockchain has a key pair:

* Public Key: can be shared with others, it's like your email address. It functions as an address where others can send transactions.
* Private Key: must be kept secret, it's like your password. It's used to digitally sign the transactions you send, proving that you are the owner of the funds.

When you make a transaction, it is signed with your private key. The network nodes can verify this signature using your public key, without needing to know your private key. This ensures that transactions are authentic and that only the legitimate owner can move the funds associated with that public key.

Cryptography also plays a crucial role in maintaining anonymity (or rather pseudonymity) in transactions. Although all transactions are public, they are associated with addresses that don't necessarily reveal the real identity of the user. However, it's important to remember that with sufficient analysis, it's possible to trace transactions and potentially identify users.

