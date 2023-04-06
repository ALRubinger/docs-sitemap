# Create a Decentralized Identifier

Before creating your DID, be sure to check out the [Quickstart guide](../../quickstart) to ensure you’ve properly imported the Web5 SDK. We also have guides to [learn more about DIDs](../../Learn/decentralized-identifiers#DID-Method).

## Create a DID

```jsx
import {Web5} from '@tbd54566975/web5'
const web5 = new Web5();
const myDid = await web5.did.create('ion');
```

When calling `create`, be sure to pass in a Web5-supported [DID method](). `create` returns a JSON representing your newly created DID, which we’ve stored in `myDid`. Here’s an example of what the `myDid` object will look like:

```json
{
   "id":"did:ion:EiD5iTx5H9P_LKxfKkAx4...",
   "internalId":"did:ion:EiD5iTx5H9P_LKxfKkAx4J5oRIAsko9RSsbOoL2sURMsSg",
   ...
   "keys":[
      {
         "id":"key-1",
         "type":"JsonWebKey2020",
         "keypair":{
            "publicJwk":{
               "kty":"EC",
               "crv":"secp256k1",
               "x":"_fhttpkgTd-icwBqoHoWrzIsULDLoM02Mv2ewFEl9_k",
               "y":"wFNaCJ27Yu7Yh4yCgYxWHI2tcWsSZ7ugnc0UYeKn2uM"
            },
            "privateJwk":{
               "kty":"EC",
               "crv":"secp256k1",
               "x":"_fhttpkgTd-icwBqoHoWrzIsULDLoM02Mv2ewFEl9_k",
               "y":"wFNaCJ27Yu7Yh4yCgYxWHI2tcWsSZ7ugnc0UYeKn2uM",
               "d":"dhQUKGtPgiVs0WOgY0frP8_5WR-tTgNbB1UI93h2iTw"
            }
         },
         "purposes":[
            "authentication"
         ]
      }
   ],
   ...
}
```

## Register DID Keys in Decentralized Web Node

When you instantiate `Web5`, the SDK internally creates a Decentralized Web Node (DWN) to act as a personal data store to store your DID keys. In order to store your DID, register it with the Web5 SDK to save and encrypt your keys.

```jsx
    web5.did.register({
      connected: true,
      did: myDid.id,
      endpoint: 'app://dwn', 
      keys: myDid.keys[0].keypair
    });
```