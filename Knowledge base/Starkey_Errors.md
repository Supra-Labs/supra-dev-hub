## Table of Contents

--------------------------------------
NOTE: Kindly follow the below format to get started with reporting the issues!
- `ISSUE SUMMARY`
- `SOLUTION SUMMARY`
- `LINK TO ISSUE (If applicable)`
--------------------------------------

## ISSUE SUMMARY: share a sample code for Starkey wallet connection in next.js

## SOLUTION SUMMARY: 

**Demo Here:** https://frontend-web-wallet-connect-demo.vercel.app/supra-dapp
**Repo:** https://github.com/Entropy-Foundation/frontend-web-wallet-connect-demo

## ISSUE SUMMARY: sign function code snippet for Wallet

## SOLUTION SUMMARY: 
signMessage accepts a hex string as message and returns object containing:
address of signer, public key, and signature

   ```PowerShell
import nacl from "tweetnacl";

 const remove0xPrefix = (hexString: string) => {
  return hexString.startsWith("0x") ? hexString.slice(2) : hexString;
 }

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
Can test in your browser dev console with the following

   ```PowerShell
 const response = await window.starkey.supra.signMessage({
    message:"0x74657374"
  });
   ```
