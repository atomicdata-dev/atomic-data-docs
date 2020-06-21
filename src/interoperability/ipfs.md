# Atomic Data and IPFS

## What is IPFS

IPFS (the InterPlanetery File System) is a standard that enables content-based identifiers.
Intead of using an HTTP URL like `http://example.com/helloworld`, it uses the IPFS scheme, such as `ipfs:QmX6j9DHcPhgBcBtZsuRkfmk2v7G5mzb11vU9ve9i8vDsL`.
It identifies things based on their unique content hash (the long, seemingly random string).
This simple idea (plus some not so simple network protocols) allows for decentalized, temper-proof storage of data.
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

## Example of Atomic Data on IPFS

Here's an example, serialized to Atomic-NDJSON:

[https://ipfs.io/ipfs/QmX6j9DHcPhgBcBtZsuRkfmk2v7G5mzb11vU9ve9i8vDsL]

```ndjson
["https://atomicdata.dev/helloworld","https://atomicdata.dev/properties/description","Hello world!"]
```

## Atomic Data and IPLD

IPLD (not IPFS) stands for InterPlanetery Linked Data, but is not related to RDF.
The scope seems fundamentally different from RDF, too, but I have to read more about this.
TODO!
