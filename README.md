# WHMCS Plugin for iRedMail Pro
Tested on WHMCS 7.2.3-release.1, PHP7, and iRedMail-Pro v2.7.0 (MySQL)

## Philosophy
Being incredibly difficult to break into self-hosting markets, the goal of this plugin is to enable developers, small business owners, and freelancers to take advantage of the powerhouses that are WHMCS and iRedMail-Pro.

## Design
Based on the iRedMail Pro design, that an administrative account exists that is responsible for multiple domains, the plugin will use WHMCS hooks to create an iRedMail administrator on WHMCS account creation and/or update. Whenever the password is changed in WHMCS, it will push the password to iRedMail via API.
Purchase of a product in WHMCS will raise the iRedMail administrator's domain capacity by +1. The domain can be billed as a separate object from users including total domain storage space.
The WHMCS server cron function will ping the iRedMail-Pro domain to parse the number of users and then utilize the WHMCS api to invoice an amount per user per hour as well as total domain storage per hour.

## Action Flow
### Administrator
#### WHMCS Account Creation
1. Check if the account exists. `iRedMail:GET /api/admin/<mail>`
    1) If it does exist, update it with zero alotted domains and zero total storage. `iRedMail:PUT /api/admin/<mail>?password=$WHMCS_USER_PASS&maxDomains=0`
    2) Get a list of domains assigned to administrator. `NOT YET IMPLEMENTED`
    3) Update WHMCS user alotted domains with product list through internal api. (This action will branch to the WHMCS Server Product Purchase function tree. The purpose of this flow is to allow for existing domains to be imported into WHMCS billing.)
        1] Get a list of products assigned to the module. `WHMCS:https://developers.whmcs.com/api-reference/getproducts/ POST:api.php?action='GetProducts'&module='WHMCS-iRedMail-Pro'`
            1} If no products are created, initialize. 
        2] Select default domain pricing setting.
        3] Use 2) to determine the number of products to add.
        4] 
        
2. If it doesn't exist, create it with zero alotted domains and zero total storage.

#### WHMCS Account Update


#### WHMCS Account Deletion


### Domain
#### WHMCS Server Product Purchase

#### WHMCS Server Product Update

#### WHMCS Server Product Deletion


### Cron
#### WHMCS Cron Run
