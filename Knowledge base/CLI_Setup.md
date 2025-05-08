## Table of Contents
1. [> Suppy Uri Value](#ISSUE-SUMMARY-Suppy-Uri-Value)

2. [> MODULE_ADDRESS_DOES_NOT_MATCH_SENDER](#ISSUE-SUMMARY-Module-address-doesnt-match-sender)

3. [> Supra Command Not Executing](#ISSUE-SUMMARY-Supra-Command-Not-Executing)

4. [> Docker Daemon Not Running](#ISSUE-SUMMARY-Docker-Daemon-Not-Running)

5. [> Supra equivalent command for create-resource-account](#ISSUE-SUMMARY-Supra-equivalent-command-for)

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

NOTE: Follow the format below to get started with reporting the issues!
- `ISSUE SUMMARY`
- `SOLUTION SUMMARY` 

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)


## ISSUE SUMMARY: Suppy Uri Value
getting value input message while installing CLI -

```bash
cmdlet Invoke-WebRequest at command pipeline position 1
Supply values for the following parameters:
Uri:
```

### ➥ SOLUTION SUMMARY:
You can use **Git Bash** instead of powershell to avoid this issue while installing CLI.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)


## ISSUE SUMMARY: Module address doesnt match sender
Module not getting deployed

 ```bash
"vm status": "MODULE_ADDRESS_DOES_NOT_MATCH_SENDER"
 ```

### ➥ SOLUTION SUMMARY:
- This is supposed to be generated CLI profile address.
- Make sure the activated profile is the same that you have set as the named address in move.toml.
- To check if it's activated - there will be a star next to it.


![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

## ISSUE SUMMARY: Supra Command Not Executing

The `supra` command does not run as expected.

```PowerShell
supra
```

### ➥ SOLUTION SUMMARY:

1. Verify that aliasing is properly set for your Docker containers.
2. Check if your Docker container is running in Docker Desktop:

   - Open Docker Desktop and ensure the container is active, or
   - Run the following command:

   ```PowerShell
   docker ps
   ```

   Ensure the supra_cli container is listed as running.

3. If the container is not running:
   - Restart the container.
   - Attempt to run the `supra` command again.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

## ISSUE SUMMARY: Docker Daemon Not Running

When running the following command:

```PowerShell
docker run --name supra_cli -v <YOUR_PATH>:/supra/configs -e SUPRA_HOME=/supra/configs --net=host -itd asia-docker.pkg.dev/supra-devnet-misc/supra-testnet/validator-node:v6.3.0
```

You may encounter the error:

`
docker: error during connect: this error may indicate that the docker daemon is not running: Post "http://%2F%2F.%2Fpipe%2Fdocker_engine/v1.24/containers/create?name=supra_cli": open //./pipe/docker_engine: The system cannot find the file specified.
`

### ➥ SOLUTION SUMMARY:

Ensure Docker Desktop is running before executing the command
Once Docker is running, retry the command.

```PowerShell
docker run --name supra_cli -v <YOUR_PATH>:/supra/configs -e SUPRA_HOME=/supra/configs --net=host -itd asia-docker.pkg.dev/supra-devnet-misc/supra-testnet/validator-node:v6.3.0
```

If the issue persists: - Confirm your Docker installation is complete. - Check that the Docker service is properly configured to start.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

## ISSUE SUMMARY: Supra equivalent command for

```PowerShell
aptos move create-resource-account-and-publish-package
```
### ➥ SOLUTION SUMMARY:
We don't have a CLI command for this directly, you call the create_resource_account function manually, here is the GitHub ref to check its execution: https://github.com/Entropy-Foundation/aptos-core/blob/dev/aptos-move/framework/supra-framework/sources/resource_account.move

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)