## BlackbaudSkyApi-FENXT
A Power BI custom data connector for the Blackbaud's Financial Edge NXT (SKY API). The connector is not owned, developed or supported by Blackbaud, and as such is defined by Power BI as an [uncertified connector](https://docs.microsoft.com/en-us/connectors/custom-connectors/submit-certification#certification-criteria). See CHANGELOG.md for recent changes.
![PBIGetData](blobs/getdata.PNG "Blackbaud FENXT SkyAPi (Beta) in Get Data").

## Getting Started
These instructions will describe how to configure the FENXT SKY API connector in order to connect to your organisation's data. See Microsoft's guide to installing and using custom data connectors in Power BI [here](https://github.com/Microsoft/DataConnectors).

You will need to create and register an application with SKY API for the purpose of generating the requisite IDs used when making a connection to your data. A Blackbaud developer account is required in order to create an application. Once an application has been created, you will need the **application_id** of the application, the **application_secret** of your application, and your developer account's **api_subscription_key**.

### Setting up a Blackbaud developer account
Follow the instructions at https://developer.blackbaud.com/skyapi/docs/getting-started to create a developer account and acquire your **api_subscription key**.

### Creating an app
Follow the instructions at https://developer.blackbaud.com/skyapi/docs/createapp to register and activate your app. Registering your app will generate a **application_id** and **application_secret** for the app. Ensure that at least one of the Redirect URLs for the app you create is set to https://oauth.powerbi.com/views/oauthredirect.html

### Installing the connector
1. If one does not already exist, create a `[My Documents]\Microsoft Power BI Desktop\Custom Connectors` directory
2. Download the FENXT.mez file from this repo, or grab the latest release from the [Releases](https://github.com/GrantQuick/BlackbaudSkyApi/releases) area and extract the contents. Place the FENXT.mez file in the `[My Documents]\Microsoft Power BI Desktop\Custom Connectors` directory.
3. Rename the FENXT.mez file to FENXT.zip
4. Open up FENXT.zip. Edit the application_id, application_secret and api_subscription_key files. In each file, copy and paste the character strings for the appropriate entity (the application_id, application_secret and api_subscription_key generated when creating a Blackbaud developer account and app) into the correct file. Save the changes to each of the three files.
5. Rename FENXT.zip back to FENXT.mez.
6. Enable the **Custom data connectors** preview feature in Power BI Desktop (under *File | Options and settings | Custom data connectors*).
7. As of the July 2018 release, Power BI will additionally alert users to change their security settings in order to enable uncertified custom data connectors to be used. To do this, go to *File | Options and settings | Security*, and under **Data Extensions**, enable **(Not Recommended) Allow any extension to load without validation or warning**.
7. Restart Power BI Desktop
8. In Power BI Desktop, click **Get Data > Other > Blackbaud FENXT SkyAPi (Beta)**
9. The first time you use the connector you will need to log in using your Blackbaud account and authorise the app to work with your data.

## Supported Endpoints
The connector supports the following endpoints:
* Account cashflow
* Account code
* Account custom field
* Account fund
* Account structure
* Account working capital
* Budget
* Budget scenario
* Cash management distribution set
* Client name
* Fiscal year
* General ledger media type
* Grant custom field
* Grant status
* Grant type
* Journal entry batch
* Journal entry custom field
* Period summary
* Project custom field
* Project department
* Project division
* Project location
* Project status
* Project type
* Transaction distribution
* Transaction distribution set
* Accounts payable department
* Accounts payable interfund set
* Accounts payable media type
* Accounts payable product
* Buyer
* Credit memo custom field
* FOB
* Invoice
* Invoice custom field
* Organization address
* Payment term
* Purchase order
* Purchase order custom field
* Ship via
* Staff
* State 1099
* Unit of measure
* Vendor
* Vendor custom field
* Bank account
* Cash receipt custom field
* Treasury media type

## Additional Information
The connector generates a basic data model. Selected list or record type data fields have been expanded, which will increase row counts where "list" datatypes are nested within records.

When using the connector, it is recommended to **only select the endpoints that are necessary for any given reporting purpose**. Endpoints that are not required as part of a specific Power BI dashboard/report should be omitted from your connection as they will introduce superfluous calls to the SKY API, and could cause throttling/quota issues.

## Scheduled Refresh - Power BI Service
The connector supports scheduled refresh through the Power BI service via a Power BI On-Premises Data Gateway (Personal mode). In order to take advantage of this, the following steps need to be performed:

1. Install the Power BI On-Premises Data Gateway in Personal mode
2. Enable Custom Connector support in the Gateway - see guide [here](https://docs.microsoft.com/en-us/power-query/samples/trippin/9-testconnection/readme)
3. Publish a workbook that uses your connector to PowerBI.com
4. Configure scheduled refresh - see guide [here](https://docs.microsoft.com/en-us/power-query/samples/trippin/9-testconnection/readme#testing-scheduled-refresh) and follow the instructions from *After publishing, go to PowerBI.com and find the dataset...*

## Known Issues
Currently several list endpoints cannot be connected to, due to inconsistencies in Blackbaud's implementation of each endpoint and the way in which they return data, or the requirement to supply individual record IDs as part of the API calls rather than being able to specify "return all data".

Depending on dataset size, data load time can be long, although Blackbaud have worked to improve the speed of call processing. As a maximum of 500 (or 5000, depending on the endpoint) records can be returned by any single call to an endpoint, datasets of several hundred thousand records will require many hundred calls to the API. The API also employs rate limiting to prevent overload of Blackbaud servers. This can mean that data loads of all endpoints will take several minutes. Connecting to only the required endpoints will reduce data load time.

## Authors
* **Grant Quick** - *Initial work* - [GrantQuick](https://github.com/GrantQuick)

## Acknowledgments
* This connector is based on the [custom data connector samples](https://github.com/Microsoft/DataConnectors) provided by [Microsoft](https://github.com/Microsoft)
* Thanks to [Graham Getty](https://resolvedllc.com) for access to resources
