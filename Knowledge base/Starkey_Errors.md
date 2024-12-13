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

## ISSUE SUMMARY: Starkey wallet or explorer Metadata retrieval for their custom token

## SOLUTION SUMMARY: 

   ```PowerShell
https://rpc-testnet.supra.com/rpc/v1/accounts/0xa9aa1587371e78286391d86d7e951cf2c177e5d48eb494387e74eefcc53d6217/resources/0x1::coin::CoinInfo%3C0xa9aa1587371e78286391d86d7e951cf2c177e5d48eb494387e74eefcc53d6217::moon_coin::MoonCoin%3E
   ```
- Coins have a CoinInfo resource.
- You query for the CoinInfo to retrieve the metadata.

When you add it to Starkey, you add it as: `a9aa1587371e78286391d86d7e951cf2c177e5d48eb494387e74eefcc53d6217::moon_coin::MoonCoin`

and the wallet will query the CoinInfo resource to grab the metadata for the token and display it in walletCoinInfo in coin.move:

- https://github.com/Entropy-Foundation/aptos-core/blob/f9652d1f0472fc60f887605ff13f[…]01b039e4/aptos-move/framework/supra-framework/sources/coin.move

## ISSUE SUMMARY: 
How to call move function in my dapp if I used Chrome StarKey wallet

## SOLUTION SUMMARY: 
The code snippet in below link demonstrate that how can we create tx payload for entry function
- https://github.com/Entropy-Foundation/supra-l1-sdk/blob/master/src/example.ts#L190 

Convert the move function call to `rawTransaction` object and pass it to the data defined on Supra & [Starkey docs](https://docs.starkey.app/) and ignore the `sequence_number` like metamask ignore the nonce and the Starkey Wallet side will process later.

## ISSUE SUMMARY: 
when I try to get the balance using sdk it shows 200000000 but in the explorer, it shows 100000000 supra coin why?

## SOLUTION SUMMARY: 
This will be displayed on Starkey but not on Suprascan. It's shown to you as output, but it will not be in RPC or Exploror. Once this is unstacked or the time of the staking is over, then when that amount is again credited to their Star Key wallet, that activity will be tracked, and then this balance will be shown on a Surprascan. But not now until you have stacked your thing.
