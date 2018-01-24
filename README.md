# fastly-postman

> Fastly API client for Postman

![Banner](/screenshots/banner.png?raw=true "Fastly API Collection for Postman")

## Problem

You always face the same problems when you need to send requests to a RESTful API:

1. How to authenticate?
2. What headers need to be sent with the request?
3. Which body properties need to be defined and which ones can be updated?

Every API handles authentication differently and the body configuration for writable endpoints is also different. Usually, the example requests of an API documentation are very simple and the [Fastly API](https://docs.fastly.com/api/) examples are no exception. Mostly you have to send multiple requests to the same endpoint in order to find out how the request needs to be properly configured!

Nowadays a lot of companies provide a [Postman](https://www.getpostman.com/) integration to their users in order to make it easy to get started. Unfortunately, Fastly doesn't provide such thing. Since the [Fastly API](https://docs.fastly.com/api/) provides more features than the application itself you need to use it to take full advantage of their service. [Postman](https://www.getpostman.com/) is a far better replacement of `cURL` and therefore it doesn't make any sense to create a collection of `cURL` commands these days!

## Solution

[Postman](https://www.getpostman.com/) allows you to configure, send, and save HTTP requests. To structure requests, you can define collections and folders. You can also define local and global variables which can be referenced in the URL, headers, and the body. The best part is that you can group local variables in environments. You can then easily switch between environments in order to reference different variables.

This repository contains a [Postman](https://www.getpostman.com/) collection and an environment for the [Fastly API](https://docs.fastly.com/api/). The body of each writeable endpoint has been preconfigured with all possible properties you are able to update and allowed to send. The goal is to make the interaction with the API as easy as possible without running and modifying `cURL` commands in the terminal. You just need to update the global and environment variables to get started. Once setup is complete, you have another powerful tool to manage your [Fastly](https://www.fastly.com/) account and services!

## Table of Contents

- [Security](#security)
- [Getting Started](#getting-started)
- [API](#api)
- [Usage](#usage)
- [Tests](#tests)
- [Contribute](#contribute)

## Security

You need a valid [API token](https://docs.fastly.com/api/auth#tokens) in order to use the [Fastly API](https://docs.fastly.com/api/). I recommend using a token with a [global scope](https://docs.fastly.com/api/auth#access) to be able to perform requests to all endpoints.

This client makes it very easy to create and manage your API tokens. You can find in the `Authentication` folder two different endpoint configurations for [POST /tokens](https://docs.fastly.com/api/auth#tokens_db4655a45a0107448eb0676577446e40):

1. Create a none limited API token (global scope).
2. Create a limited API token (local scope). The token can be limited by a service, an expiration, and a scope access level.

## Getting Started

These instructions will get you a copy of all the necessary `JSON` configuration files you need to import into [Postman](https://www.getpostman.com/).

### Prerequisites

You need [Postman](https://www.getpostman.com/) in order to get started. You can either add the [Postman Extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en-US) to your [Chrome](https://www.google.com/chrome/browser/desktop/index.html?brand=CHBD&gclid=CIHNlY--r9ICFUaNfgodSrEJFg) web browser or you can download the free [Postman Application](https://www.getpostman.com/).

### Downloading

There are several ways you can get the `JSON` configuration files:

#### Cloning The GitHub Repository

The recommended way is to use `git` to directly clone the repository:

```bash
$ git clone https://github.com/philippschulte/fastly-postman
```

This will clone the latest version to a `fastly-postman` folder.

#### Downloading The Repository Zip File

Another way is to download a zip copy from the [master branch on GitHub](https://github.com/philippschulte/fastly-postman/archive/master.zip). You can also do this using the `wget` command:

```bash
$ wget https://github.com/philippschulte/fastly-postman/archive/master.zip -O fastly-postman.zip; unzip fastly-postman.zip; rm fastly-postman.zip; mv fastly-postman-master fastly-postman
```

### Install

Open [Postman](https://www.getpostman.com/) and click on the [Import](#usage) button on the top bar and drag and drop:

```
fastly.postman_collection.json
fastly.postman_environment.json
fastly.postman_globals.json
```

## API

Below is a list of all the supported libraries of the [Fastly API](https://docs.fastly.com/api/):

| Category                 	| Coverage 	|
|--------------------------	|----------	|
| Authentication           	| 100%     	|
| Account                  	| 67%      	|
| Configuration            	| 100%     	|
| Purging                  	| 100%     	|
| Historical stats         	| 100%     	|
| Real-time analytics      	| 0%       	|
| Remote logging           	| 0%       	|
| Utilities                	| 100%     	|
| Web Application Firewall 	| 0%       	|
| Dynamic Servers          	| 0%       	|

## Usage

1. Click on the `Manage Environments` button and then on the `Globals` button at the bottom of the window. Update all global variables with your account information. The `username` and `password` fields are only necessary if you want to create API Tokens. **Don't change the variable names unless you want to update all request configurations!**

![Update Global Variables](/screenshots/usage_1.png?raw=true "Update Global Variables")

2. Click on the `Manage Environments` button and select the `Fastly` environment. Rename the environment. It probably makes sense to use the `service name` or the `service ID` to name your environments. Update all environment variables with your service information. **Please do yourself a favor and don't update the variable names! If you do change them you'll need to update all request configurations!** Keep in mind that you can add as many variables as you want to your environment. To use a variable you need to enclose the variable name with double curly braces – `{{my_variable_name}}`. You can reference your variables in headers, body, and tests.

![Update Environment Variables](/screenshots/usage_2.png?raw=true "Update Environment Variables")

3. Click on the `Manage Environments` button and then click the `Duplicate Environment` button to create an environment for each of your services. Select each environment to update the name and the values for `service_id`, `service_name`, and `version_no`. Within this window you can also export or delete and environment.

![Duplicate Environments](/screenshots/usage_3.png?raw=true "Duplicate Environments")

4. Take a look at the screenshot below to get familiar with the basic Postman functionality. The Postman application has a very intuitive UI but in case you are looking for more information please look at their [docs](https://www.getpostman.com/docs/). You can find all the necessary request information in the description section. **Each request description provides a link to redirect you to the associated Fastly documentation! You can find the link at the bottom of the description section.**

![Basic Postman Functionality](/screenshots/usage_4.png?raw=true "Basic Postman Functionality")

5. Another great feature of [Postman](https://www.getpostman.com/) is that you can generate code snippets for cURL and most server-side languages. All you need to do is to click on the `Generate Code Snippets` link and select your favorite language. **This feature is awesome because your environment variables are replaced with their corresponding values! Technically there are no changes necessary in order to send the requests from you scripts!**

![Generate Code Snippets](/screenshots/usage_5.png?raw=true "Generate Code Snippets")

Don't forget that you can always customize this collection and environment to meet your needs like:

1. [Managing collections](https://www.getpostman.com/docs/postman/collections/managing_collections)
2. [Adding requests](https://www.getpostman.com/docs/postman/sending_api_requests/requests)
3. [Adding new variables to your environments like surrogate keys](https://www.getpostman.com/docs/postman/environments_and_globals/variables)
4. [Adding test scripts](https://www.getpostman.com/docs/postman/scripts/test_scripts)

**Always hit the `Save` button whenever you make changes you want to persist and don't forget to select the proper environment from the drop-down list before you fire any requests!**

## Tests

With [Postman](https://www.getpostman.com/) you can write and run tests for each request using the JavaScript language. [Postman](https://www.getpostman.com/) allows you to loop through the data returned by an API and perform sequential requests and tests using that data.

It contains a powerful runtime based on [Node.js](https://nodejs.org/en/) that allows you to add dynamic behavior to requests and collections. This allows you to write test suites, build requests that can contain dynamic parameters, pass data between requests, and a lot more. You can add JavaScript code to execute during 2 events in the flow:

1. Before a request is sent to the server, as a [pre-request script](https://www.getpostman.com/docs/postman/scripts/pre_request_scripts) under the Pre-request Script tab.
2. After a response is received, as a [test script](https://www.getpostman.com/docs/postman/scripts/test_scripts) under the Tests tab.

Whatever code you write in these sections is executed in the [Postman Sandbox](https://www.getpostman.com/docs/postman/scripts/postman_sandbox). To check what is available in the sandbox, take a look at their [docs](https://www.getpostman.com/docs/postman/scripts/postman_sandbox). Postman tries to make the process easier by listing commonly used snippets next to the editor. You can select the snippet you want to add and the appropriate code will be added to the test editor. This is a great way to quickly build test cases.

Results are displayed in a `Tests` tab under the response viewer. The tab header shows how many tests passed, and the keys that you set in the tests variable are listed here. If the value evaluates to true, the test passed.

![Postman Sandbox](/screenshots/usage_6.png?raw=true "Postman Sandbox")

The [Postman Collection Runner](https://www.getpostman.com/docs/postman/collection_runs/starting_a_collection_run) allows you to run either the entire collection or a single library against a corresponding environment. **Don't forget to select an environment before you run your tests!**

![Postman Collection Runner](/screenshots/usage_7.png?raw=true "Postman Collection Runner")

I know that a lot of Fastly users build their own scripts to automate requests to the Fastly API. [Postman’s Newman Tool](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman) allows you to run and test a Postman Collection directly from the command line. It is built with extensibility in mind so that you can easily integrate it with your continuous integration servers and build systems.

For instance, if you want to run your assertions for the `Dictionary` library in the terminal, you just need to type:

```
$ newman run fastly.postman_collection.json -e fastly.postman_environment.json -g fastly.postman_globals.json --folder Dictionary
```

![Postman’s Newman Tool](/screenshots/usage_8.png?raw=true "Postman’s Newman Tool")

**I have added to each request at least one assertion to test the status code. I wanted to keep the collection as simple as possible! Feel free to add as many assertions to the collection as you like!**

## Contribute

PRs accepted. I am open to suggestions in improving this library.

## License

Licensed under the [MIT License](LICENSE) © 2017 Philipp Schulte
