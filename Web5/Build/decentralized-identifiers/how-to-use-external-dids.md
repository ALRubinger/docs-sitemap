# Use an external DID in Web5

Although `Web5` offers everything you need to create your own `did`, you may want to use an externally-created `did` in your application instead. For example, you could use a module like `ssi-service` to generate your own `did` outside of your `Web5` application and then bring it over to use in your app.

Using `Web5`, you’d normally create a `did` and then save it using the following code:

```jsx
import {Web5} from '@tbd54566975/web5'

const web5 = new Web5();
const myDid = await web5.did.create('ion');

// Save your newly created DID in your DWN
web5.did.register({
      connected: true,
      did: myDid.id,
      endpoint: 'app://dwn', 
      keys: myDid.keys[0].keypair
    });
```

In order to bring an external DID into your `Web5` project, simply replace the `myDid` object you created using `Web5` with the `did` data of the `did` you’d like to import. The structure of `myDid` is as follows:

```jsx
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

## Importing a DID from ssi-service

If you’d like to practice importing a `did` created outside of `Web5`, you can do so by creating a `did` using the `ssi-service` library as follows:

```jsx
// This is how to bring your own key. You can create a key from the ssi service and import it into the dwn
const web5 = new Web5();

const myDidSSI = await ssisdk.createDIDKey()
const keypair = {
      id: "key-1",
      type: "JsonWebKey2020",
      keypair: {
        publicJwk: myDidSSI.publicJWK,
        privateJwk: myDidSSI.privateJWK
      },
      purposes: [
        "authentication"
      ]
    }

web5.did.register({
      connected: true,
      did: myDidSSI.didDocument.id,
      endpoint: 'app://dwn',
      keys: keypair
    });
```

As long as the `ssi-service` and `Web5` instances that are creating the keys live in the same application, this is perfectly safe to do. If, however, you have a separate application running `ssi-service` that generates a `did`, export that `did` to plain text or some other more portable format, and attempt to import that `did` document into your app, you’d be doing so in an unsafe manner.