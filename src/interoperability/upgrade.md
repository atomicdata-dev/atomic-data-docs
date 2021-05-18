# Upgrade your existing application to Atomic Data

If you want to make your existing project compatible with Atomic Data, you probably don't have to get rid of your existing storage / DB implementation.
The only thing that matters, is how you make the data accessible to others: the serialization.
You can keep your existing software and logic, but simply change the last little part of your API.
In short, this is what you'll have to do:

- Map all properties of resources to Atomic Properties. Either use existing ones, or create new ones and make them accessible (using any Atomic Server, as long as the URLs of the properties resolve).
- Make sure that when the user requests some URL, that you return that resource as a JSON-AD object (at the very least if the user requests it using an HTTP `Accept` header).

Don't feel obliged to implement all parts of the Atomic Data spec, such as Collections and Commits.
