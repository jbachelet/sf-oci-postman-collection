# Salesforce OCI - Commerce API POSTMAN Collection

This folder contains a sample POSTMAN collection that you can leverage to understand how the Salesforce Omni Channel Inventory endpoints are working using the Commerce API, and can be used to operate with your Salesforce Omni Channel Inventory instance.

## :gear: Get started

In order to start with this collection, please follow these steps:

1. Download POSTMAN from the [official website](https://www.postman.com/downloads/) and installed it
2. Once installed, open POSTMAN
3. Once opened, import the collection and the environment from this repository to your POSTMAN workspace
4. Once imported, open the `Salesforce OCI - Commerce API` environment, and modify all the data which contain placeholders (like `<YOUR-CLIENT-ID-HERE>`) with your details. Please **don't modify the values with `{{` and `}}`, as these values are calculated values within your POSTMAN environment.**. The environment also contains sample values that you can use, or modify, as per your needs.
5. Once the environment is setup, open the `Salesforce OCI - Commerce API` collection, and start using it.

## :gear: Where do I find these setup values?

**Please note the official implementation guide is available [here](https://resources.docs.salesforce.com/latest/latest/en-us/sfdc/pdf/salesforce_omnichannel_inventory_implementation_guide.pdf).**

### client_id and client_password

The `client_id` environment variable is the Client ID generated within the Salesforce B2C Account Manager. The `client_password` is the password tied to the client ID.
In order to generate it, please do the following steps:
1. Go to https://account.demandware.com
2. Go to the `API Client` menu
3. Click on the `Add API Client` button
4. Fill out a Display Name and a Password. The password you enter here corresponds to the `client_password` environment variable.
5. As roles, please select the `Salesforce Commerce API` role on the Salesforce B2C Commerce instance you want to test OCI against with.
6. In the OpenID allowed scopes, add the Omnichannel Inventory scopes. The complete list is available [here](https://developer.salesforce.com/docs/commerce/commerce-api/guide/auth-z-scope-catalog.html).
7. Select `client_secret_post` as Token Endpoint Auth Method.
8. Select `JWT` as Access Token Format
9. Click on save.
10. Once saved, the client ID is generated, please use this value for the `client_id` environment variable.

### short_code

The `short_code` environment variable is the Salesforce Commerce API short code tied to your OCI setup. This value is available in the Salesforce Core org on which you want to run Omnichannel Inventory.
In order to find the value, please do the following steps:
1. Go to your Salesforce Core org.
2. Click on the gear icon on the top left and go to the `Setup` menu
3. Ensure that the `Omnichannel Inventory` toggle is `on` within the `Omnichannel Inventory` menu of the setup (use the Quick Find box to access to it.)
4. If the setting is on, on the same page you'll find the `Base URL for Inventory API Calls`, please use the subdomain from this URL. For example if the URL is `https://US.api.commercecloud.salesforce.com`, then use `US`.
5. If the setting is off, please switch it on, then reload the page, you'll see the `Base URL for Inventory API Calls` value.

### tenant_group_id

The `tenant_group_id` environment variable is the Salesforce Tenant group ID that is tied to your Salesforce Core org and your Omnichannel Inventory instance.
In order to find that value, please do the following steps:
1. Go to your Salesforce Core org.
2. Click on the gear icon on the top left and go to the `Setup` menu
3. Ensure that the `Omnichannel Inventory` toggle is `on` within the `Omnichannel Inventory` menu of the setup (use the Quick Find box to access to it.)
4. If the setting is on, on the same page you'll find the `Tenant Group ID`, please use this value for the `tenant_group_id` environment variable.
5. If the setting is off, please switch it on, then reload the page, you'll see the `Tenant Group ID` value.

### realm_id

The `realm_id` corresponds to the 4 letters realm identifier of your realm. This ID is provided by the Salesforce B2C support team when initializing the realm. Please us this value for the `realm_id` environment variable.
This value is also the first part of the On-demand sandboxes hostnames.
For example, if the sandbox hostname is `aaaa-001.sandbox.us01.dx.commercecloud.salesforce.com`, the `realm_id` is `aaaa`.
Also, another way to find this `realm_id` is to extract it from the Salesforce Commerce APIs Organization ID. In order to find it, you can do the following:
1. Go to the Business Manager of the instance
2. Go to the `Administration >  Site Development >  Salesforce Commerce API Settings` menu.
3. On the page, you'll see the `Organization ID` label.
4. This organization ID is composed of `f_ecom_{realm_id}_{instance_id}`. You can use the `realm_id` piece of this value in your environment variable.

### instance_id

The `instance_id` corresponds to the name of the instance.
For On-demand sandboxes, it is the number after the realm ID.
For example, if the sandbox hostname is `aaaa-001.sandbox.us01.dx.commercecloud.salesforce.com`, the `instance_id` environment variable is `001`.
For regular sandboxes and PIG instances, use the first part of the hostname as identifier.
For example, for a staging instance where the hostname is `http://staging-podname-client.demandware.net`, please use `stg` as the `instance_id` environment variable (you can use `dev` for `development` and `prd` for `production`).
For example, for a regular sandbox instance where the hostname is `http://dev01-podname-client.demandware.net`, please use `s01` as the `instance_id` environment variable.
Also, another way to find this `instance_id` is to extract it from the Salesforce Commerce APIs Organization ID. In order to find it, you can do the following:
1. Go to the Business Manager of the instance
2. Go to the `Administration >  Site Development >  Salesforce Commerce API Settings` menu.
3. On the page, you'll see the `Organization ID` label.
4. This organization ID is composed of `f_ecom_{realm_id}_{instance_id}`. You can use the `instance_id` piece of this value in your environment variable.

## :information_source: Description

This collection contains use-case based sub-collections. The collection is divided into three main components, `AVAILABILITY`, `IMPEX`, and `RESERVATIONS`, in order to reflect how the documentation on the [Salesforce Developer Portal](https://developer.salesforce.com/docs/commerce/commerce-api/references) is done.

Within these folders, you'll find a sub-collection per use case, which contains the list of endpoints which can be used to perform the desired operation and validate that the operation worked.

![POSTMAN Collections screenshot](imgs/POSTMAN-Collection-Overview.png "POSTMAN Collections screenshot")

All endpoints contain unit tests, which allows the collection to ensure:

:white_check_mark: The endpoints respond with the correct data/behavior based on the use-case

:white_check_mark: The API is working as expected, by validating the data before/after some operations (like reservations or availability updates), to ensure the API is doing what we expect

## :rocket: How to?

### How to generate the file to be used in the IMPEX > Import Inventory Records use case?

In order to send the file containing the records, you need to GZIP it, then get the hash of the file to provide it in the API calls of the use case.

#### GZIP the file through bash

In order to GZIP the file, you can use the following command in bash:

```bash
gzip <path/to/file.json>
```

This will generate a GZIP archive of the given file.
#### Get the hash of the file through bash

In order to get the has of the file, you can use the following command in bash:

```bash
openssl dgst -sha256 <path/to/file.json>
```

This will give you a hash of the file that you need to use in the `impex_file_hash` environement variable.

### How to use the collection?

You can leverage this collection in differente ways:

:arrow_forward: By using any endpoint one-by-one. Please remember to always authenticate first, by using any of the authentication endpoint available within the use-case collections.

:arrow_forward: Note that all API calls anotated with `(Optional)` are not required in a production use. These calls are there to show and test that the API works as expected.

![POSTMAN One Endpoint Sample screenshot](imgs/POSTMAN-Sample.png "POSTMAN One Endpoint Sample screenshot")

:next_track_button: By using the [POSTMAN Runner](https://learning.postman.com/docs/running-collections/intro-to-collection-runs), which will run a full use-case directly, by executing each endpoint one-by-one, sequentially, and so report the unit tests results for each executed endpoint.
:warning: **When running a use-case, please put a minimum of 1000ms delay between each endpoint execution, as I've seen some unit-tests not passing when a request was executed to quickly after another. I guess this is due to some sort of cache within the Salesforce Omni Channel Inventory system in my sandbox environment**.

![POSTMAN Runner Sample screenshot](imgs/POSTMAN-Runner-Sample.gif "POSTMAN Runner Sample screenshot")