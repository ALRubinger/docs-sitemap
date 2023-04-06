# Read from Decentralized Web Nodes

Before reading from your Decentralized Web Node (DWN), be sure to check out our [Quickstart guide](../../quickstart) to ensure you’ve properly imported the Web5 SDK. Additionally, make sure you’ve set up a DID before attempting to read from a DWN.

## Read from a DWN

The following snippet allows you to read from your `Web5` instance’s DWN:

```jsx
// Query for the record that was just created.
const queryResponse = await web5.dwn.records.query(myDid.id, {
  author: myDid.id,
  message: {
    filter: {
      schema: 'schema.org/foo/bar'
    }
	}
});
```

The read `request` must contain the following:

- **`author`** - *`string`*: The decentralized identifier of the DID signing the query. This may be the same as the `target` parameter if the target and the signer of the query are the same entity, which is common for an app querying the DWeb Node of its own user.
- **`message`** - *`object`*: The properties of the DWeb Node Message Descriptor that will be used to construct a valid DWeb Node message. `schema` must be a resolvable
- **`filter`** - *`object`*: an object that defines a set of properties to filter results.
    - **`protocol`(optional)** - *`URI string`*: a URI that represents the protocol being queried for.
    - **`schema`(optional)** - *`URI string`*: a URI that represents the schema being queried for.