--------------------------------------
NOTE: Kindly follow the below format to get started with reporting the issues!
- `ISSUE SUMMARY`
- `SOLUTION SUMMARY`
- `LINK TO ISSUE`
--------------------------------------

## ISSUE SUMMARY: If a request fails on callback, is there a time-delay before it is retried?

### SOLUTION SUMMARY:
Depends on the type of failure. There can be a lot of reasons for the failure.
If the client has insufficient balance then its going to get failed after 3 retries from each primary and backup. So we send multiple emails alerts before the client balance reaches minBalance. 
If the delay is because of txn not getting confirmed yet and still in the mempool (because of the gas price) then we do retry twice with a span of 3 mins  from each primary and backup.
If the failure is because of some revert actions present in the client contract then we provide proper events to tranck them.

NOTE:: Backup node works 15 blocks behind primary


## ISSUE SUMMARY: Is there a time window where, after a certain amount of retries or some time period, the request is permanently dropped? 

### SOLUTION SUMMARY:
No specific time window in this version that will be available in the next version.

## ISSUE SUMMARY: If Chainlink ever fails its callback (due to insufficient funds or whatever the case may be), we're able to rescue funds from the game contract itself, knowing that after 24 hours, that specific request will never try to callback again. I was wondering if we had any guarantees in this way for Supra, so we know how to handle an event of something going wrong.

### SOLUTION SUMMARY:
For Chainlink if it fails only due to insufficient balance then it keeps the request for 24 hrs. They do that because they dont have restrictions while accepting the request but we dont accept any request if the client balance reaches the min balance but we serve the responses of accumulated requests that were in queue.

## ISSUE SUMMARY: Pull Oracles are returning 404.

### SOLUTION SUMMARY:
Using the code present in the master branch, Please ask follow this one: https://github.com/Entropy-Foundation/oracle-pull-example/tree/feat/DoraV2/rest/javascript

## ISSUE SUMMARY: getting below caution for dVRF.
"Supra dVRF V2 requires subscription to the service with a customer controlled wallet address to act as the main reference.
Therefore you must register your wallet with the Supra team if you plan to consume Supra dVRF V2 within your smart contracts.
Please refer to the Supra documentation for the latest steps on how to register your wallet for their service.".

### SOLUTION SUMMARY:
It means you have to whitelist your address with Supra Team and then use dVRF.
