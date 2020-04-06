[![Build Status](https://travis-ci.com/laodemalfatih/i18next-node-mongo-backend.svg?branch=v0.0.3-dev)](https://travis-ci.com/laodemalfatih/i18next-node-mongo-backend)
[![Maintainability](https://api.codeclimate.com/v1/badges/5fc60912b2776f1e1a53/maintainability)](https://codeclimate.com/github/laodemalfatih/i18next-node-mongo-backend/maintainability)
[![codecov](https://codecov.io/gh/laodemalfatih/i18next-node-mongo-backend/branch/master/graph/badge.svg)](https://codecov.io/gh/laodemalfatih/i18next-node-mongo-backend)

[![npm](https://badgen.net/npm/v/i18next-node-mongo-backend?color=red)](https://www.npmjs.com/package/i18next-node-mongo-backend)
[![npm downloads](https://badgen.net/npm/dt/i18next-node-mongo-backend)](https://www.npmjs.com/package/i18next-node-mongo-backend)
[![license](https://badgen.net/npm/license/i18next-node-mongo-backend)](https://github.com/laodemalfatih/i18next-node-mongo-backend/blob/master/LICENSE)

#### Inspired from [i18next-node-mongodb-backend](https://github.com/gian788/i18next-node-mongodb-backend) with support for `mongodb@3.5.x` and some bug fixes and more improvements

# Integrate [i18next](https://github.com/i18next/i18next) with [MongoDB](https://www.mongodb.com/)

<img src="assets/i18next.png" alt="I18next Logo" width="100"/><img src="assets/mongodb.png" alt="MongoDB Logo" width="330" style="margin-left: 25px;"/>

# Introduction

This is a [i18next](https://github.com/i18next/i18next) backend to be used Node JS. It will load resources from a [MongoDB](https://www.mongodb.org) database with official node mongodb [driver](https://mongodb.github.io/node-mongodb-native/3.5/).

# Getting started

```bash
yarn add mongodb i18next-node-mongo-backend
# or
npm install mongodb i18next-node-mongo-backend
```

> Important: This library doesn't include `mongodb` library. You have to install it yourself

# Usage

```js
const i18next = require('i18next');
const Backend = require('i18next-node-mongo-backend');

i18next
  .use(Backend)
  .init({
    // Backend Options
    backend: options
  });
```

# Backend Options

```js
{
  // Required field

  dbName: '<DB Name>',
  // Collection name in database will be used to store i18next data
  collectionName: 'i18n',

  // If you have your own `MongoClient`, put in here:
  // Note: If this has already been entered, the other MongoDB configurations will be ignored
  client: new MongoClient(), // work with connected client or not

  // Or (Choose one)

  // MongoDB standard configuration
  host: '127.0.0.1',
  port: 27017,

  // MongoDB authentication. Remove it if not needed
  user: '<User>',
  password: '<Password>',

  // MongoDB field name
  languageFieldName: 'lang',
  namespaceFieldName: 'ns',
  dataFieldName: 'data',

  // If false, then the database connection will be closed every time the i18next event completes
  persistConnection: false,

  // Error handlers
  readOnError: console.error,
  readMultiOnError: console.error,
  createOnError: console.error,

  // MongoClient Options. See https://mongodb.github.io/node-mongodb-native/3.5/api/MongoClient.html
  mongodb: {
    useUnifiedTopology: true
  }
};
```

> We do not provide `uri` options. You just fill out the available options, we will do it automatically for you

## Example of the MongoDB document that will be created:
```json
// Key name is according to provided in options
{
  "lang" : "en-US",
  "ns" : "translations",
  "data" : {
    "key": "Thank you!"
  }
}
```

# Change Log:

## v0.0.3:

  - Add testing with [Jest](https://jestjs.io/)
  - Add [JSDOC](https://jsdoc.app/)
  - Some improvements