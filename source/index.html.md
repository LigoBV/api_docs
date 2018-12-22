---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - php

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: false
---

# Introduction

Welcome to the Ligo API! Automate your documents with Ligo! Generate, track
revisions, sign, organize, download and more directly from your own 
applications and tools.

We have language bindings in Shell, Ruby, and Php! You can view code examples 
in the dark area to the right, and you can switch the programming language of 
the examples with the tabs in the top right.


# Authentication

> To authorize, use this code:

```ruby
require "ligo_api"

LigoApi.client_id = "my_client_id"
LigoApi.client_secret = "my_client_secret"
```

```php
<?php

$client_id = "my_client_id";
$client_secret = "my_client_secret"
\LigoApi\Ligo::setClientCredentials($client_id, $client_secret);

```

```shell
curl -X POST \
  'https://ligo.nl/oauth/token?client_id=my-client-id&client_secret=my-client-secret&grant_type=client_credentials' \
  -H 'cache-control: no-cache'


# You can then use the received access_token as an authorization Bearer token
# in the headers. You will need to manage token rotation manually. 
```

> Make sure to replace `client_id` and `client_secret` with your API key.

Ligo uses API keys to allow access to the API. You can register a new Ligo API 
key at our [developer portal](https://ligo.nl/developers).

Ligo is built on oAuth 2.0. The client credentials are exchanged for short 
lived access tokens to the API. Our API Libraries will handle the rotation
for you. It is best to install these where the app boots to prevent 
instantiating on every request.

<aside class="notice">
You must replace <code>client_id</code> and <code>client_secret</code> with 
your personal API key.
</aside>

# Suppliers

## Get All Suppliers

```ruby
suppliers = LigoApi::Supplier.all
```

```php
<?php

$suppliers = \LigoApi\Supplier::all();
$supplier = $suppliers[0];
$supplier->name;
```

```shell
curl -X GET \
  https://www.ligo.nl/api/suppliers \
  -H 'Authorization: Bearer your-bearer-token'
```

> The above command returns JSON structured like this:

```json
{
  "suppliers": [
    {
      "id": "19b5e45d-3974-48c4-896f-21341a32e793",
      "name": "Supplier 1"
    },
    {
      "id": "19b5e45d-3974-48c4-896f-21341a32e793",
      "name": "Supplier 2"
    },
  ]
}
```

This endpoint retrieves all suppliers. Suppliers are a record intended to 
organize your contracts. If you are purchasing an item or a service from a 
party it is best to add it as a supplier.

### HTTP Request

`GET https://www.ligo.nl/api/suppliers`


## Get a Specific Supplier

```ruby
suppliers = LigoApi::Supplier.find(id)
```

```php
<?php 

$supplier = \LigoApi\Supplier::find("2083e5f8-61f5-4726-beda-5ca9d7224a25");
$supplier->name; // My Supplier
```

```shell
curl -X GET \
  https://ligo.nl/api/suppliers/19b5e45d-3974-48c4-896f-21341a32e793 \
  -H 'Authorization: Bearer your-bearer-token' \

# replace the id with the id of the supplier
```

> The above command returns JSON structured like this:

```json
{
  "supplier": {
    "id": "19b5e45d-3974-48c4-896f-21341a32e793",
    "name": "My Supplier"
  }
}
```

This endpoint retrieves a specific supplier.

# Customers

## Get All Customers

```ruby
suppliers = LigoApi::Customer.all
```

```php
<?php

$customers = \LigoApi\Customer::all();
$customer = $customers[0];
$customer->name;
```

```shell
curl -X GET \
  https://www.ligo.nl/api/customers \
  -H 'Authorization: Bearer your-bearer-token'
```

> The above command returns JSON structured like this:

```json
{
  "customers": [
    {
      "id": "19b5e45d-3974-48c4-896f-21341a32e793",
      "name": "Customer 1"
    },
    {
      "id": "19b5e45d-3974-48c4-896f-21341a32e793",
      "name": "Customer 2"
    },
  ]
}
```

This endpoint retrieves all customers. Customers are a record intended to 
organize your contracts. If you are selling an item or a service from a 
party it is best to add it as a customer.

### HTTP Request

`GET https://www.ligo.nl/api/customers`


## Get a Specific Customer

```ruby
customer = LigoApi::Customer.find(id)
customer.name # My Customer
```

```php
<?php 

$customer = \LigoApi\Customer::find("2083e5f8-61f5-4726-beda-5ca9d7224a25");
$customer->name; // My Customer
```

```shell
curl -X GET \
  https://ligo.nl/api/customers/19b5e45d-3974-48c4-896f-21341a32e793 \
  -H 'Authorization: Bearer your-bearer-token' \

# replace the id with the id of the customer
```

> The above command returns JSON structured like this:

```json
{
  "customer": {
    "id": "19b5e45d-3974-48c4-896f-21341a32e793",
    "name": "My Customer"
  }
}
```

This endpoint retrieves a specific customer.

# Contract Templates

Contract templates are created within your Ligo Dashboard. Each type of 
contract is identified by a unique slug called <code>template_type</code>. For
each template type you may have a variety of contracts based on country and
language. For instance, you may have an NDA for the Netherlands in English and
Dutch as well as an NDA for Spain in Spanish. You will need to determine
which contract template you want to use when creating a contract.

## Get All Contract Templates

```ruby
templates = LigoApi::ContractTemplate.all
template = templates.first
template.name
```

```php
<?php

$templates = \LigoApi\ContractTemplate::all();
$template = $templates[0];
$template->name;
```

```shell
curl -X GET \
  https://www.ligo.nl/api/contract_templates \
  -H 'Authorization: Bearer your-bearer-token'
```

> The above command returns JSON structured like this:

```json
{
  "contract_templates": [
    {
        "id": "f36214d7-4cd5-4b62-9ba8-55b1f1e9dcc8",
        "name": "Oproepcontract 0 uren Engels",
        "country": "nl",
        "language": "en",
        "template_type": "zero_hours_employment_agreement",
        "created_at": "2018-11-20T10:13:25.143+01:00",
        "updated_at": "2018-12-09T12:23:39.139+01:00"
    },
    {
        "id": "263f505c-938e-45c6-ad00-d7f9c5c08d6a",
        "name": "Mobile Phone Agreement",
        "country": "NL",
        "language": "nl",
        "template_type": "mobile_phone_agreement",
        "created_at": "2018-10-25T18:45:06.494+02:00",
        "updated_at": "2018-12-09T12:23:39.221+01:00"
    }
  ]
}
```

This endpoint retrieves all your contract templates. You can use this to 
determine which template you want to use when generating a contract. You can
either identify a contract based on <code>template_type</code>, 
<code>language</code>, and <code>country</code> or the <code>id</code> of the
template.

### HTTP Request

`GET https://www.ligo.nl/api/contract_templates`


## Get a Specific Contract Template

```ruby
template = LigoApi::ContractTemplate.find(id)
template.name # Mobile Phone Agreement
```

```php
<?php 

$template = \LigoApi\ContractTemplate::find($id);
$template->name; // Mobile Phone Agreement
```

```shell
curl -X GET \
  https://ligo.nl/api/contract_templates/19b5e45d-3974-48c4-896f-21341a32e793 \
  -H 'Authorization: Bearer your-bearer-token' \

# replace the id with the id of the customer
```

> The above command returns JSON structured like this:

```json
{
  "contract_template": {
    "id": "90cf8619-5244-4cf0-ba68-5085377ef736",
    "name": "Laptop Agreement",
    "country": "nl",
    "language": "en",
    "template_type": "laptop_agreement",
    "created_at": "2018-11-26T14:37:30.861+01:00",
    "updated_at": "2018-12-09T12:23:39.147+01:00"
  }
}
```

This endpoint retrieves a specific contract template.

# Contracts

The contracts endpoint allows you to merge your templates with data from your
own application. Once we create the document, Ligo will handle everything else
for you. We will return the contract to you in HTML form immediately. It could
take up to a few minutes for the documents in word and pdf format as well as
preview images to generate. We will send you a notification when it is done!

## Get a specific contract

```ruby
contract = LigoApi::Contract.find(id)
contract.name
```

```php
<?php

$contract = \LigoApi\Contract::find($id);
$contract->name;
```

```shell
curl -X GET \
  https://www.ligo.nl/api/contracts/my-id-of-the-contract \
  -H 'Authorization: Bearer your-bearer-token'
```

> The above command returns JSON structured like this:

```json
{
    "contract": {
        "id": "da94452e-a5f2-4d27-b468-90c534c0c627",
        "content": "<p>This is my document in HTML form</p>",
        "created_at": "2018-12-22T03:28:36.248+01:00",
        "documents_generating": true,
        "expiration_date": null,
        "name": "Your custom name here",
        "pdf_document_url": null,
        "pdf_signed_document_url": null,
        "png_image_url": null,
        "updated_at": "2018-12-22T03:28:36.248+01:00",
        "word_document_url": null
    }
}
```

This endpoint will return details about a specific template. Since document and
image generation may take a few moments after creating some of the data may
at first be blank. You can use our webhooks to ensure you get updated as soon
as your documents are ready. 

### HTTP Request

`GET https://www.ligo.nl/api/contracts/my-contract-id`


## Create a Contract

```ruby
params = {
  name: "My Contract Name",
  template_id: "955744b4-fbe8-49b0-930b-a725597f8714",
  participants: $participants,
  context: { 
    variable_1: "this is your variable",
    variable_2: { 
      liquid: "we use liquid for templating, you can use nested hashes too"
    },
    counts: [
      "arrays work as well", 
      "another string", 
      "yet another string"
    ]
  }
}

contract = LigoApi::Contract.create(params)
```

```php
<?php 

$participants = array(
  0 => array( "type" => "Customer", "id" => "d74b9f62-5fb4-48e2-ac58-b77b213a2d3f"), 
  1 => array( "type" => "Supplier", "id" => "19b5e45d-3974-48c4-896f-21341a32e793"),
);

$params = array(
  "name" => "My Contract Name",
  "template_id" => "955744b4-fbe8-49b0-930b-a725597f8714",
  "participants" => $participants,
  "context" => array(
    "variable_1" => "this is your variable",
    "variable_2" => array(
      "liquid" => "we use liquid for templating, you can use nested hashes too"
    ),
    "counts" => array_values(
      array("arrays work as well", "another string", "yet another string")
    )
  )
);

\LigoApi\Contract::create($params);
```

```shell
curl -X POST \
  http://ligo.local:3000/api/contracts \
  -H 'Authorization: Bearer your-bearer-token' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{ 
        "contract": {
          "name": "Your custom name here",
          "template_type": "my_custom_contract",
          "language": "en",
          "country": "nl",
          "template_id": "955744b4-fbe8-49b0-930b-a725597f8714",
          "participants": [
            { "type": "Customer", "id": "d74b9f62-5fb4-48e2-ac58-b77b213a2d3f" },
            { "type": "Supplier", "id": "19b5e45d-3974-48c4-896f-21341a32e793" }
          ],
          "context": {
            "variable_1": "these are your custom variables",
            "liquid": {
              "nesting": "we use liquid for templating, you can use nested hashes too"
            },
            "counts": ["arrays work as well", "another string", "another string"]
          }
        } 
      }
  '
```

> The above command returns JSON structured like this:

```json
{
  "contract": {
    "id": "da94452e-a5f2-4d27-b468-90c534c0c627",
    "content": "<p>This is my contract in html format</p>",
    "created_at": "2018-12-22T03:28:36.248+01:00",
    "documents_generating": true,
    "expiration_date": null,
    "name": "Your custom name here",
    "pdf_document_url": null,
    "pdf_signed_document_url": null,
    "png_image_url": null,
    "updated_at": "2018-12-22T03:28:36.248+01:00",
    "word_document_url": null
  }
}
```

This endpoint creates a contract. When creating a contract you can give it an
expiration date. You will receive webhooks when the contract is expiring. 

Contracts can also be tied to other entities like Employees, Suppliers and 
Customers. This allows organization directly within the Ligo dashboard and the
ability to quickly search and filter the contracts. See the appropriate 
sections for more details on creating these objects.

Document generation for contracts does not happen immediately. To prevent long
request times these are processed asynchronously. It is possible to set up
the webhooks to receive events at which point you can retrieve the documents.
