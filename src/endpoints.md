# Atomic Endpoints

_URL: https://atomicdata.dev/classes/Endpoint_

An Endpoint is a resource that accepts parameters in order to generate a response.
You can think of it like a function in a programming language, or a API endpoint in an OpenAPI spec.
It can be used to perform calculations on the server side, such as filtering data, sorting data, selecting a page in a collection, or performing some calculation.
Because Endpoints are resources, they can be defined and read programmatically.
This means that it's possible to render Endpoints as forms.

The most important property in an Endpoint is [`parameters`](https://atomicdata.dev/properties/endpoint/parameters), which is the list of Properties that can be filled in.

You can find a list of Endpoints supported by Atomic-Server on [atomicdata.dev/endpoints](https://atomicdata.dev/endpoints).

## Design Goals

- **Familiar API**: should look like something that most developers already know
- **Auto-generate forms**: a front-end app should present Endpoints as forms that non-developers can interact with

[Discussion in issue tracker](https://github.com/ontola/atomic-data-docs/issues/15).
