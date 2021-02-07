# Atomic Data and IPFS

## What is IPFS

IPFS (the InterPlanetary File System) is a standard that enables decentralized file storage and retrieval using content-based identifiers.
Instead of using an HTTP URL like `http://example.com/helloworld`, it uses the IPFS scheme, such as `ipfs:QmX6j9DHcPhgBcBtZsuRkfmk2v7G5mzb11vU9ve9i8vDsL`.
IPFS identifies things based on their unique content hash (the long, seemingly random string) using a thing called a Merkle DAG ([this great article](https://medium.com/textileio/whats-really-happening-when-you-add-a-file-to-ipfs-ae3b8b5e4b0f#:~:text=In%20practice%2C%20content%20addressing%20systems,function%2C%20to%20produce%20a%20digest.&text=From%20raw%20image%20to%20cryptographic%20digest%20to%20content%20id%20(multihash).) explains it nicely).
This is called a [CID](https://github.com/multiformats/cid), or Content ID.
This simple idea (plus some not so simple network protocols) allows for decentralized, temper-proof storage of data.
This fixes some issues with HTTP that are related to its centralized philosophy: no more 404s!

## Why is IPFS especially interesting for Atomic Data

Atomic Data is highly dependent on the availability of Resources, especially Properties and Datatypes.
These resources are meant to be re-used a lot, and that would make everything expensive.

## Considerations using IPFS URLs

They are static, their contents can never change.
This is great for some types of data, but horrible for others.
If you're describing a time-dependent thing (such as a person's job),
If you're describing personal, private information, its also a bad idea to use IPFS, because it's designed to be permanent.
Also, IPFS is not as fast as HTTP - at least for now.

## Atomic Data and IPLD

IPLD (not IPFS) stands for InterPlanetary Linked Data, but is not related to RDF.
The scope seems fundamentally different from RDF, too, but I have to read more about this.
