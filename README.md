# Etherfi Sync Client
The Etherfi Sync Client is a tool designed to simplify the process of accessing validator keys for Node Operators who have won auctions.

## Build and Use
* `go mod tidy`
* `make`
* `./etherfi-sync-clientv2`

## Remove files and executable
* `make clean`

## Remote Setup, Build, Use
On remote computer, make directory for sync client and curl the executable from url:  https://github.com/GadzeFinance/etherfi-sync-clientv2/releases
```shell
# create directory and go inside it
mkdir sync-client
cd sync-client

# grab the executable from github
curl -LJO https://github.com/GadzeFinance/etherfi-sync-clientv2/releases/download/v1.0.4/<file-name-specified-in-release-table>

# unpack the executable
tar -xf <file-name-specified-in-release-table>

# make a new output directory for stake bids that have been won
mkdir output

# make sure you create create "keys" and "passwords" dicrectory in the OUTPUT_LOCATION path
mkdir -p ${OUTPUT_LOCATION}/keys
mkdir -p ${OUTPUT_LOCATION}/passwords

# create configuration file
touch config.json

# edit the configuration file based on the config.json from here:
# https://github.com/GadzeFinance/etherfi-sync-clientv2/blob/master/config.json
```
```json
{
	"GRAPH_URL": (ask it to ether.fi team),
	"IPFS_GATEWAY": (ask it to ether.fi team),
	"BIDDER": (your node operator wallet),
	"OUTPUT_LOCATION": (the path you want to download the keys to),
	"PRIVATE_KEYS_FILE_LOCATION": (the path to your `privateEtherfiKeystore-….json`),
	"PASSWORD": (the passwd you used when generating the private keys via etherfi-desktop-app),
	"IGNORE_LAST_VALIDATOR_INDEX": (boolean, set true to ignore the local database and iterate over all validator bids from thegraph)
}
```

## How to make a release
1. Checkout into the master branch
2. Run `git pull origin master` to make sure you have all the changes
3. Update the `tag_name` and `release_name` in `.github/workflows/makerelease.yaml` to the new version of the release
4. Commit your changes
5. Go to the actions page in the github repo
6. Click on `Create Release with Binary` in the side bar
7. Trigger the workflow using the `Run Workflow` button
> Note: Pushes to the master branch will trigger a release

