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

# Generating URI with Pinata

**Pinata** is a platform that facilitates file storage in **IPFS** (InterPlanetary File System). We'll use Pinata to host your NFTs' images and metadata in IPFS, obtaining a **Base URI** that you can use in your ERC721 contract.

**1. Create a Pinata Account**

* Visit [Pinata](https://www.pinata.cloud/) and sign up for a free account. This account will allow you to upload and manage files on IPFS.

{% embed url="https://www.pinata.cloud/" %}

**2. Upload your NFTs' Images to Pinata**

* In your Pinata account, select **"Add"** and choose **"File Upload"** to upload each image individually or in batch.

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

* When you upload an image, Pinata will generate a **CID** (Content Identifier), which is a unique identifier that represents that image in IPFS.
* **Note**: Save the CID of each image, as you'll need it to include it in the `image` field of each NFT's metadata.

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

**3. Create JSON Metadata Files**

Each NFT needs a JSON metadata file containing its unique information, such as name, description, and image link. Here's an example of how a metadata JSON file for an NFT would look:

```json
{
  "name": "NFT #1",
  "description": "This is NFT number 1 from my collection",
  "image": "ipfs://[image_CID]",
  "attributes": [
    {
      "trait_type": "Color",
      "value": "Red"
    },
    {
      "trait_type": "Type",
      "value": "Wizard"
    }
  ]
}
```

* **`image` field**: Replace `[image_CID]` with the CID of the corresponding image in IPFS. For example, if the image's CID is `QmXyz123`, the `image` field should be `"ipfs://QmXyz123"`.
* **Attributes**: You can include any attributes you want, such as specific characteristics or rarity levels. You can leave it empty or add more.

**4. Create a Metadata Folder and Upload it to Pinata**

To facilitate access to all metadata from the same base URI, organize all JSON files in a **folder**. Then:

* Upload the complete folder with the JSON metadata files to Pinata by selecting **"Add"** > **"Folder Upload"**.
* Once you upload the folder, Pinata will generate a unique **CID** for the folder.

5.  **Get the Base URI**

    The folder's CID becomes your **Base URI** for the NFT collection. The format of this base URI will be something like:

    ```arduino
    ipfs://[folder_CID]/
    ```

    When you configure this **Base URI** in your ERC721 contract, you can access specific NFT metadata by adding the corresponding `tokenId` at the end. For example:

    * `ipfs://[folder_CID]/1` will be the link for the NFT with `tokenId` 1.
    * `ipfs://[folder_CID]/2` for the NFT with `tokenId` 2, and so on.

### Your turn

Upload 3 random images to Pinata and then upload a folder with their Metadata. We'll use the folder's CID for the NFTs we create.
