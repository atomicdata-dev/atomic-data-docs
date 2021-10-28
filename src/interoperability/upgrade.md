{{#title Upgrade your existing application to Atomic Data}}
# Upgrade your existing application to Atomic Data

If you want to make your existing project compatible with Atomic Data, you probably don't have to get rid of your existing storage / DB implementation.
The only thing that matters, is how you make the data accessible to others: the serialization.
You can keep your existing software and logic, but simply change the last little part of your API.
In short, this is what you'll have to do:

- Map all properties of resources to Atomic Properties. Either use [existing ones](https://atomicdata.dev/properties), or [create new ones](https://atomicdata.dev/app/new?classSubject=https%3A%2F%2Fatomicdata.dev%2Fclasses%2FProperty&parent=https%3A%2F%2Fatomicdata.dev%2Fagents%2F8S2U%2FviqkaAQVzUisaolrpX6hx%2FG%2FL3e2MTjWA83Rxk%3D&newSubject=https%3A%2F%2Fatomicdata.dev%2Fproperty%2Fsu98ox6tvkh) and make them accessible (using any Atomic Server, as long as the URLs of the properties resolve).
- Make sure that when the user requests some URL, that you return that resource as a JSON-AD object (at the very least if the user requests it using an HTTP `Accept` header).

Don't feel obliged to implement all parts of the Atomic Data spec, such as Collections and Commits.

If you need any help, get in touch in our [Discord](https://discord.gg/a72Rv2P)
