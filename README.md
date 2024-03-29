# daml-sample
DAML blockchain sample code
 
[![Daml logo](https://daml.com/static/images/logo.png)](https://www.daml.com)

[![Download](https://img.shields.io/github/release/digital-asset/daml.svg?label=Download)](https://docs.daml.com/getting-started/installation.html)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/digital-asset/daml/blob/main/LICENSE)

# Welcome to _Daml-Sample_

This repository contains a template to get started with developing full-stack
[Daml](https://daml.com/) applications. The demo application covers the following aspects:

1. A [Daml](https://docs.daml.com/index.html) model of a simple social network
2. A UI written in [TypeScript](https://www.typescriptlang.org/) and [React](https://reactjs.org/)

The UI is developed using [React](https://reactjs.org/),
[Semantic UI](https://react.semantic-ui.com/) and its
official [React integration](https://react.semantic-ui.com/).
The whole project was bootstrapped with
[Create React App](https://github.com/facebook/create-react-app).
Regardless of these choices, all Daml specific aspects of the UI client are
written in plain TypeScript and the UI framework should hence be easily
replaceable.


## Getting started

Before you can run the application, you need to install the
[Node](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) package manager for JavaScript.

There are two steps to build the project.
First, we need to generate TypeScript code bindings for the compiled Daml model.
At the root of the repository, run
```
daml build
daml codegen js .daml/dist/daml-sample-0.1.0.dar -o ui/daml.js
```
The latter command generates TypeScript packages in the `daml.js` directory.

Next, navigate to the `ui` directory and install the dependencies and build the app by running
```
cd ui
npm install
npm run-script build
```
The last step is not absolutely necessary but useful to check that the app compiles.

To start the application, there are again two steps.
In one terminal in the root directory, start a Daml ledger using
```
daml start
```
This must continue running to serve ledger requests.

Then in a second terminal window in the `ui` directory, start the UI server via
```
npm start
```
This should open a browser window with a login screen.
If it doesn't, you can manually point your browser to http://localhost:3000.


## A quick tour

You can log into the app by providing a user name, say `Alice`. For simplicity
of this app, there is no password or sign-up required. You will be greeted by
a screen indicating that you're not following anyone and that you don't have
any followers yet. You can change this by following someone in the upper box,
say `Bob`. After that, let's log out in the top right corner and log in as `Bob`.

As `Bob`, we can see that we are not following anyone and that `Alice` is follwing
us. We can follow `Alice` by clicking the plus symbol to the right of here name.


## Deploying to Daml Hub

Deploying `daml-sample` to the hosted Daml platform
[Daml Hub](https://hub.daml.com/) is quite simple. Log into your Daml Hub
account, create a new ledger and upload your Daml models and your UI.

To upload the Daml models, compile them into a DAR by executing
```
daml build -o daml-sample.dar
```
at the root of your repository. Afterwards, open to the Daml Hub website, select
the ledger you want to deploy to, go to the "Daml" selection and upload the
DAR `daml-sample.dar` you have just created.

To upload the UI, create a ZIP file containing all your UI assets by executing
```
daml build
daml codegen js .daml/dist/daml-sample-0.1.0.dar -o ui/daml.js
(cd ui && npm install && npm run-script build && zip -r ../daml-sample-ui.zip build)
```
at the root of the repository. Afterwards, select the "UI Assets" tab of your
chosen ledger on the Daml Hub website, upload the ZIP file
(`daml-sample-ui.zip`) you have just created and publish it.

To see your deployed instance of `daml-sample` in action, follow the
"Visit site" link at the top right corner of your "UI Assets" page.


## Next steps

There are many directions in which this application can be extended.
Regardless of which direction you pick, the following files will be the most
interesting ones to familiarize yourself with:

- [`daml/User.daml`](daml/User.daml): the Daml model of the social network
- `daml.js/daml-sample-0.1.0/src/User.ts` (once you've generated it):
  a reflection of the types contained in the Daml model in TypeScript
- [`ui/src/components/MainView.tsx`](ui/src/components/MainView.tsx):
  a React component using the HTTP Ledger API and rendering the main features


## Useful resources

TBD


## How to get help

TBD
