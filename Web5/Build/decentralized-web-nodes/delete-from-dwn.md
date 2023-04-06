# Delete Data from a Decentralized Web Node

Before deleting from your Decentralized Web Node (DWN), be sure to check out our Quickstart page to ensure you’ve properly imported the Web5 SDK. Additionally, make sure you’ve set up a DID before attempting to delete from a DWN.

## Deleting from a DWN

```jsx
const recordId = queryResponse.entries[0].recordId
const deleteResponse = await web5.dwn.records.delete(myDid.id, {
  author: myDid.id,
  message: {
     recordId: recordId
  }
});
```

The delete `request` must contain the following:

- **`author`** - *`string`*: The decentralized identifier of the DID signing the query. This may be the same as the `target` parameter if the target and the signer of the query are the same entity, which is common for an app querying the DWeb Node of its own user.
- **`message`** - *`object`*: The prrties of the DWeb Node Message Descriptor that will be used to construct a valid DWeb Node message.
    - **`recordId`** - *`string`*: the required record ID string that identifies the record being deleted.