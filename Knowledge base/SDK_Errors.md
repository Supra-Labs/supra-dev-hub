NOTE: Kindly follow the below format to get started with reporting the issues!
- `ISSUE SUMMARY`
- `SOLUTION SUMMARY`
- `LINK TO ISSUE`
--------------------------------------

## ISSUE SUMMARY: 
Contract integration for contracts deployed on supra and integrated with client-side using supra sdk

## SOLUTION SUMMARY: 
Relevant Links:
- https://sdk-docs.supra.com/classes/SupraClient.html
- https://github.com/Entropy-Foundation/supra-l1-sdk/blob/master/src/example.ts

## ISSUE SUMMARY: 
Type error: Cannot find module `supra-l1-sdk` or its corresponding type declarations.

## SOLUTION SUMMARY: 
This issue could be resolved by defining `commonjs` acceptance in `next.config.js`.

Supra have made changes in the support branch as well for this so devs don't have to do this: 
- https://github.com/Entropy-Foundation/supra-l1-sdk/tree/support-ledger-wallet

Devs can check the commits of 9th Dec'24 to check the changes made in that branch to replicate the same in your side of the code.

## ISSUE SUMMARY: 
In aptos sdk we have aptos.getAccountModule to check the module name do we have in supra sdk to check getAccountModule?

## SOLUTION SUMMARY:
The get account info function here returns the accounts auth key and sequence number:
- https://sdk-docs.supra.com/classes/SupraClient.html#getAccountInfo

also u can check deployed module via API:

```
https://rpc-testnet.supra.com/rpc/v1/accounts/{address}/modules/{module_name}
```

## ISSUE SUMMARY: 
how to verify signature using supra SDK?

## SOLUTION SUMMARY:
- https://sdk-docs.supra.com/classes/SupraAccount.html#verifySignature

Here is a link to the verifySignature function code from the `SupraAccount` class (imported from AptosAccount): 

- https://github.com/Entropy-Foundation/aptos-core/blob/c5087137d9c9a85975c368894a24ae647fc49285/ecosystem/typescript/sdk/src/account/aptos_account.ts#L170C1-L179C4

## ISSUE SUMMARY: 
In a NextJS application, Facing a Type error: Cannot find module 'supra-l1-sdk' or its corresponding type declarations.

## SOLUTION SUMMARY:
Update the `tsconfig` file, Change `moduleResolution` from `bundler` to `node`

```
"moduleResolution": "node",
```
It will still have a warning, but The build will be working. 

Below is the warning you will get:
```
The generated code contains 'async/await' because this module is using "topLevelAwait".
However, your target environment does not appear to support 'async/await'.
As a result, the code may not run as expected or may cause runtime errors.

Import trace for requested module:
./src/libs/supra.ts
```
