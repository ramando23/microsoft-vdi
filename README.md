# Azure Creative Cloud VDI Infrastructure


Click to deploy Azure environment with guidance, designed to provide Creative Cloud Desktops in a client's existing or new subscription. Using a set of custom tools clients will be able to deploy a customisable Creative Desktops in Azure Infrastructure for up to five users in a single region with shared storage. This provides a client with a minimal commitment but viable solution for testing or small-scale use.

## Getting Started

These instructions will help you deploy Creative Cloud desktop infrastructure environments within Azure.  By providing a simple repeatable approach, teams can deliver Creative Cloud desktop infrastructure quickly and efficiently, tailored to defined personas in the creative industry.

The deployment process will deploy end user workstations up to a maximum of 5 based upon how many users are specified during this process.


## Prerequisites

There are a number of prerequisites you must have to successfully deploy this infrastructure.

**Pre-requisites:. Teradici CAM License (PCoIP registration code)**

* In order to proceed with the deployment a valid Teradici subscription should be active.
* If you require to purchase a subscription visit their website here (link).
* Teradici will provide a registration code which will be utilised in the deployment, ensure you have this to hand
* **Ensure internet explorer has been run at least once and the initial setup prompt has been actioned on the machine the Deploy script is run from.**
* Ensure Powershell execution polices have been set to allow the script the run [https:/go.microsoft.com/fwlink/?LinkID=135170](https://go.microsoft.com/fwlink/?LinkID=135170). Example:  *Set-ExecutionPolicy -ExecutionPolicy Unrestricted*


**Pre-requisites: Storage Account Key**


* In order to access the demo assets and VM image, the script will request a storage key- this will be provided to you by Microsoft. You will be unable to successfully deploy the demo resources without this key. Please ensure you have this key available prior to deploying the script.


**CAM Pre-requisite: **
Create the CAM service account

* Go to [https://cam.teradici.com](https://cam.teradici.com/) and log in
* Click on your user account in the top right of the screen
* Choose ‘CAM Service Account’ from the drop down selector
* Click ‘+’
* Enter a friendly name for the account and click ‘CREATE’
* Ensure you make a note of the **Username** and the **API key** when presented. You will require this later.

Example string:
{"keyId":"5f1021ef7240ed006725918b",**"username":"**_*5f1021ef7240ed006725918b*_**"**,**"apiKey":**_*"eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJvaWQiOiI1ZjBjYTcwY2M4NmI1YzAwMTJkYWVjYmQiLCJvd25lck9pJYR6IjE5Zjk5M2NjLTdlYTctNDJkNS1iYTc1LTA5OTY0MWJmYjg3OCIsImp0aSI6Ijk1ZDJmMDhlLWI2YTktNGZiNC05Y2Q5LWZiM2JkZDU5YTYxOSIsImlhdCI6MTU5NDg5Mjc4NSwiZXhwIjoxNjg5NTAwNzg1fQ.1X62a0wha-yq0xeWzkxO3GkLSDa2TRdioWYL1dHMIDNC15dmspIZP7vfFdaq8PmAJnefS_kT6SULPM0—QwPpA*_**"**,"keyName":"TestDeploy"}

From the API String copied out of the CAM portal you need to only use the sections highlighted in blue above

**Example of how to format information for use within the Deploy script:**

**Username:** 5f1021ef7240ed006725918b

**API key:**
eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJvaWQiOiI1ZjBjYTcwY2M4NmI1YzAwMTJkYWVjYmQiLCJvd25lck9pJYR6IjE5Zjk5M2NjLTdlYTctNDJkNS1iYTc1LTA5OTY0MWJmYjg3OCIsImp0aSI6Ijk1ZDJmMDhlLWI2YTktNGZiNC05Y2Q5LWZiM2JkZDU5YTYxOSIsImlhdCI6MTU5NDg5Mjc4NSwiZXhwIjoxNjg5NTAwNzg1fQ.1X62a0wha-yq0xeWzkxO3GkLSDa2TRdioWYL1dHMIDNC15dmspIZP7vfFdaq8PmAJnefS_kT6SULPM0—QwPpA


## Deployment

**Download the deployment script here** (GitHub link goes here)

**Run the script from a Powershell run as current logged in user**

NOTE: This script cannot be situated too deep within subfolders else the script will error flagging a 248 character limit

`C:\path\to\deploy.ps1`


You will be prompted to log into your Microsoft Azure account. This should be an account that has the correct permissions to create resources in the destination subscription.

Once authenticated you will be asked which subscription you wish to deploy.

**Type the corresponding number to the desired subscription and hit return.**

`Please choose the account number: `

**You’ll be prompted to enter your CAM PCoIP Registration code collected in Pre-Requisite 1.**

`CAM PCOIP Registration code:`

**You’ll be prompted for the CAM Service account credentials gathered in the CAM pre-requisite**

* Enter the **username **and hit return
* Enter the **API Key** and hit return


You will be asked if you’d like to create a user account. Each user account created here will have a corresponding machine created. The users defined here will be created in the Active Directory. *A workstation will be created for each unique user up to a maximum of 5 workstations.*

**Enter a username for the user you’d like to create**

`Username prompt: persona1`

**Enter a password for the user account**

`Password: <Enter Password here>`

**Enter a first name for the user account**

`First name: Persona`

**Enter a last name for the user account**

`Last name: One`

**Choose whether you’d like to create another account at this time**

`Prompt: Do you want to add a user? n`


**Enter your chosen password for the Active Directory Administrator account**

```
var.ad_admin_password
Password for the Adminstrator user

  Enter a value:<password>
```


**Enter the Access Key for the Storage Account (please see: [Pre-requisites: Storage Account Key](https://quip.com/ZkTLALODGE4h#CZSACAltRjZ) ).**


```
var.assets_storage_account_key
Access key for storage account containing demo assets and VM images

Enter a value:<storage account key>
```



**Enter your chosen password for the Cloud Access Connector Local Administrator account**

```
var.cac_admin_password
  Password for the Administrator of the Cloud Access Connector VM

  Enter a value:<password>
```

**Enter the Azure Region where you would like to deploy the resources**

```
var.location
  The Azure Region in which all resources in this example should be created.

  Enter a value:northeurope
```

**Enter your chosen password for the Directory Services Restore Mode**

```
var.safe_mode_admin_password
  Safe Mode Admin Password (Directory Service Restore Mode - DSRM)

  Enter a value:<password>
```

**Enter your chosen password for the Local Administrator account of the deployed workstations**

```
var.windows_std_admin_password
  Password for the Administrator of the Workstation

  Enter a value:<password>
```


You’ll now be asked if you’d like to proceed. From this point on, objects will begin to be created in your Azure subscription.

By scrolling up the output, the script will indicate the number of resources that will be created as part of the deployment- for example the below excerpt indicates that the deployment will create 57 resources, change 0 resources and destroy (delete) 0 resources- this is typical of a new deployment. 
Although the number or resources added will depend on the version of the script run, the number of items listed under ‘change’ or ‘destroy’ in a new deployment will be 0.

![Plan](Images/Plan.png)

 Type ‘**yes**’ if you are happy to proceed and hit return.


```
Do you want to perform these actions?
Terraform will perform the actions described above.
Only 'yes' will be accepted to approve.

Enter a value:` yes`
```


The deployment process will now begin as the Azure environment is created **(process can take approx 30mins to complete)**

On completion the script will output the following:

![Plan](Images/ApplyComplete.png)

## Errors with resource creation

If the resource required is not available in the region selected you will see an error resembling the following:

![Plan](Images/Error.png)

If Internet Explorer has never been run from the workstation you are running the script you will received the following error:

*ERROR: The response content cannot be parsed because the Internet Explorer engine is not available*


## Testing the deployment has been successful


**Check the Teradici connector health:**

Go to https://cam.teradici.com/app/connectors

The deployed connector should be in the list as healthy for both **HEALTH** and **CERTIFICATE EXPIRY. **
Please note that once the script has completed, the Teradici connector can take an additional 15-20 minutes to complete. If the connector is reported as ‘unhealthy’ refresh the page after this time has elapsed.

Make note of your **External IP **that has been allocated to the connector. You’ll need this to connect to a workstation in the next section

**Check the Teradici workstation(s):**

Go to https://cam.teradici.com/app/remoteWorkstations

The deployed workstation(s) should be listed. They should be marked as managed and running.
When you click on a workstation it should list the users authorised (assigned) to use that workstation under the heading **MANAGE USER ENTITLEMENTS FOR WORKSTATION**

By design, there is a one-to-one mapping between users and workstations. For example; if 3 users are requested during the script deployment, 3 machines will be also created, one workstation for each user created. You will be able to review user/ workstation assignments here.

## Connecting to a workstation

**To access via Teradici PCoIP client:**

* Download the latest PCoIP software for your operating system here: https://docs.teradici.com/find/product/software-and-mobile-clients
* Install the application & run on your local machine
* To set up a new connection to a workstation, click on 'new connection' 
* Enter in the external IP (You can get the External IP of the connector here https://cam.teradici.com/app/connectors)
* Enter connection name - This is a friendly name and can be anything the user chooses
* Hit 'save' and it will then ask you to 'connect insecurely'  click 'ok'
* It will then ask you for a username and password for the workstation (This will be a user account defined in the deployment process)

**The connection can take up to 5 minutes to initiate depending if the remote workstation is already running or not**

## Connecting to Active Directory

As part of the deployment, an Active Directory server will be installed and configured for the purposes of the demo. The Active Directory server will hold demo user and computer objects as well as group policies to simplify configuration.

Typically access to Active Directory will not be necessary, however, instructions to enable RDP access to the  Active Directory server are detailed below.

**Please note**, to better secure demo resources, RDP access to the Active Directory server is only granted to the public IP address from which the template was deployed.

To enable RDP access from an other public IP to Active Directory  you will need to configure the Azure Network Security Group (NSG), deployed as part of the demo, with the required details.

**Add a public IP address to the demo Network Security Group (NSG).**
The NSG will start with the prefix of ‘nsg-vdidemo-’ and will be followed by three numbers, ‘###’.

To add a new public IP, locate the NSG.
Under ‘**Inbound security rules**’ select ‘**AllowRDP**’
under ‘**Source IP address**’ add the IP ensuring that you separate any additional IP with a comma- example image below:



![Plan](Images/RDP1.png)
![Plan](Images/RDP2.png)


## Built With

* Powershell - The scripting language used to initiate the Teraform deployment and pass through the variables
* Teraform - SaaS application used to deploy infrastructure as code
* Azure - The cloud platform utilised for hosting the infrastructure
* Teradici - The applications used to broker and provide low latency remote connections to workstations


## Authors

* Support Partners - [https://www.support-partners.com](https://www.support-partners.com/)

## License

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE

This project is licensed under the MIT License - see the [LICENSE.md](https://github.com/AzEditorialWkGrp/VDI/blob/master/LICENSE.md) file for details


## Acknowledgments

* Teradici - GitHub https://github.com/teradici
* 






