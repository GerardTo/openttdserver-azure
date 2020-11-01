[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FGerardTo%2Fopenttdserver-azure%2Fmain%2FazureDeploy.json)

# Description
Deploy an [OpenTTD](https://www.openttd.org/) server to Azure.

This template should allow you to host a dedicated server and play with friends for hours, while keeping the cost under 1 Euro.

# Template

## ARM Template
The template is based on the [Linux Simple VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux) quick start template, with the below modifications:
- Open port 3979
- Run cloud-init from github

## Cloud-init
- Install OpenTTD 1.10.3
- Update a few settings in the configuration file
- Run the server

## Server Settings
| Header        | Setting            | Value                    |
|---------------|--------------------|--------------------------|
| network       | server_name        | My OpenTTD 1.10.3 Server |
| network       | rcon_password      | icontrol                 |
| network       | min_active_clients | 1                        |
| locale        | currency           | NLG                      |
| currency      | to_euro            | 1                        |

# Usage
## Pre-requisites
- Azure Subscription

## Steps
### Before playing
1. Click the **Deploy to Azure** button at the top of this page
1. Set parameters (resource group, VM credentials), and deploy
1. Go to your VM and find the IP or DNS name

### During playing
1. Launch OpenTTD, go to multiplayer, add server and past the IP or DNS name
   - It might take a couple of minutes for the server to start after the VM comes online
1. To update settings (probably a good idea), use the default rcon password: **icontrol**
   - Set password for joining the server to **letmein**: `rcon icontrol "server_password letmein"`
   - Update the rcon password to **newpassword**: `rcon icontrol "rcon_password newpassword"`

### After playing
1. When done playing, remove the resource group
   - This is to prevent incurring unneccesary costs. You can spin-up a new server in minutes when you need it again.

## Notes
- This does not support saving/loading games
- The server does not auto-shutdown, if you don't shut it down you will continue to incur costs for VM, storage, data transfer. The cost for this VM is 29,55 Euro per month
