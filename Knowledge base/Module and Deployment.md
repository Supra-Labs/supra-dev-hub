--------------------------------------
NOTE: Kindly follow the below format to get started with reporting the issues!
- `ISSUE SUMMARY`
- `SOLUTION SUMMARY`
- `LINK TO ISSUE`
--------------------------------------
## ISSUE SUMMARY: how to call move function in my dapp if I used  chrome starKey wallet

### SOLUTION SUMMARY:
The code snippet in here demonstrate that how can we create tx payload for entry function: https://github.com/Entropy-Foundation/supra-l1-sdk/blob/master/src/example.ts#L190

So we should convert the move function call to rawTransaction object  and pass it to the data that defined on your docs, and we ignore the sequence_number like metamask ignore the nonce and the wallet side will process that.

For raw transaction, Process to create a `rawTx` and `serializedRawTx` is almost similar

```PowerShell
     // To send serialized transaction
  console.log(
    await supraClient.sendTxUsingSerializedRawTransaction(
      senderAccount,
      supraCoinTransferSerializedRawTransaction,
      {
        enableTransactionSimulation: true,
        enableWaitForTransaction: true,
      }
    )
  ); 
```

## ISSUE SUMMARY: Couldn't find any docs regarding sign a message using starkey wallet, any example code that I can start with?

### SOLUTION SUMMARY:
Please update to Min V 1.1.24, This Version and Above includes the signMessage function.
Here's a code snippet for the help: 

```Javascript
import nacl from "tweetnacl";

const haxString = '0x' + Buffer.from(signMessage, 'utf8').toString('hex')
const response = await supraProvider.signMessage({message:haxString})
console.log('signMessage response :: ', response)
    if (response) {
      const { publicKey,signature,address } = response
      const sign =remove0xPrefix(signature)
      const key =remove0xPrefix(publicKey)
      const verified = nacl.sign.detached.verify(
          new TextEncoder().encode(signMessage),
          Uint8Array.from(Buffer.from(sign, 'hex')),
          Uint8Array.from(Buffer.from(key, 'hex')),
      );
     console.log('signature :: ',signature)
     console.log('verified :: ',verified)
   }
```

```Typescript
 const remove0xPrefix = (hexString: string) => {
    return hexString.startsWith("0x") ? hexString.slice(2) : hexString;
  }
```
### Demo LINK: https://frontend-web-wallet-connect-demo.vercel.app/supra-dapp

## ISSUE SUMMARY: getting error in deploying the contract to testnet while the contracts are build without any error and error code in output is 0x1::resource_account: 0x60001

### SOLUTION SUMMARY:
This error message typically indicates a problem with resource account management within the Move code. In the context of deploying a contract, it likely means that there's an issue with how your contract interacts with the resource accounts.

The current recommendation is to use objects over resources accounts iirc: https://aptos.dev/en/build/smart-contracts/deployment
Also, Check this - https://docs.supra.com/l1/rest-api/accounts/resources#rpc-v1-accounts-address-resources

For Error code 1 of resource_account module, ECONTAINER_NOT_PUBLISHED
https://github.com/Entropy-Foundation/aptos-core/blob/b414eadb54e8e8722e58096f96dab17a11787646/aptos-move/framework/supra-framework/sources/resource_account.move#L170

It means the container resource that stores the mapping of the resource address to signer capability doesn't exist at the address you are passing

Here is a repo that I used to test the create_resource_account_and_publish_package method 
https://github.com/nolan-supra/TS-SDK_Create-Resource-Account-And-Publish-Package
