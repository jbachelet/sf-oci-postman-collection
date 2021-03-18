# Salesforce Omni channel Inventory POSTMAN Collection

This repository contains a sample POSTMAN collection that you can leverage to understand how the Salesforce Omni Channel Inventory endpoints are working, and can be used to operate with your Salesforce Omni Channel Inventory instance.

## :gear: Get started

In order to start with this collection, please follow these steps:

1. Download POSTMAN from the [official website](https://www.postman.com/downloads/) and installed it
2. Once installed, open POSTMAN
3. Once opened, import the collection and the environment from this repository to your POSTMAN workspace
4. Once imported, open the `Salesforce Omni Channel Inventory` environment, and modify all the data which contain placeholders (like `<YOUR-CLIENT-ID-HERE>`) with your details. Please **don't modify the values with `{{` and `}}`, as these values are calculated values within your POSTMAN environment.**
5. Once the environment is setup, open the `Salesforce Omni Channel Inventory` collection, and start using it.

## :information_source: Description

This collection contains use-case based sub-collections. The collection is divided into three main components, `AVAILABILITY`, `IMPEX`, and `RESERVATIONS`, in order to reflect how the documentation on the [Salesforce Commerce Cloud Developer Center](https://developer.commercecloud.com/s/commerce-api-apis) is done.

Within these folders, you'll find a sub-collection per use case, which contains the list of endpoints which can be used to perform the desired operation and validate that the operation worked.

![POSTMAN Collections screenshot](https://github.com/jbachelet/sf-oci-postman-collection/blob/master/POSTMAN-Collection-Overview.png "POSTMAN Collections screenshot")

All endpoints contain unit tests, which allows the collection to ensure:

:white_check_mark: The endpoints respond with the correct data/behavior based on the use-case

:white_check_mark: The API is working as expected, by validating the data before/after some operations (like reservations or availability updates), to ensure the API is doing what we expect

## :rocket: How to?

You can leverage this collection in differente ways:

:arrow_forward: By using any endpoint one-by-one. Please remember to always authenticate first, by using any of the authentication endpoint available within the use-case collections.

![POSTMAN One Endpoint Sample screenshot](https://github.com/jbachelet/sf-oci-postman-collection/blob/master/POSTMAN-Sample.png "POSTMAN One Endpoint Sample screenshot")

:next_track_button: By using the [POSTMAN Runner](https://learning.postman.com/docs/running-collections/intro-to-collection-runs), which will run a full use-case directly, by executing each endpoint one-by-one, sequentially, and so report the unit tests results for each executed endpoint.
:warning: **When running a use-case, please put a minimum of 1000ms delay between each endpoint execution, as I've seen some unit-tests not passing when a request was executed to quickly after another. I guess this is due to some sort of cache within the Salesforce Omni Channel Inventory system in my sandbox environment**.

![POSTMAN Runner Sample screenshot](https://github.com/jbachelet/sf-oci-postman-collection/blob/master/POSTMAN-Runner-Sample.gif "POSTMAN Runner Sample screenshot")