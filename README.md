# generator-api

[![CircleCI](https://circleci.com/gh/ndelvalle/generator-api.svg?style=svg)](https://circleci.com/gh/ndelvalle/generator-api)
[![bitHound Overall Score](https://www.bithound.io/github/ndelvalle/generator-api/badges/score.svg)](https://www.bithound.io/github/ndelvalle/generator-api)
[![bitHound Dependencies](https://www.bithound.io/github/ndelvalle/generator-api/badges/dependencies.svg)](https://www.bithound.io/github/ndelvalle/generator-api/master/dependencies/npm)
[![bitHound Dev Dependencies](https://www.bithound.io/github/ndelvalle/generator-api/badges/devDependencies.svg)](https://www.bithound.io/github/ndelvalle/generator-api/master/dependencies/npm)
[![bitHound Code](https://www.bithound.io/github/ndelvalle/generator-api/badges/code.svg)](https://www.bithound.io/github/ndelvalle/generator-api)
[![npm](https://img.shields.io/npm/v/generator-api.svg?maxAge=2592000?style=flat-square)](https://www.npmjs.com/package/generator-api)

[![NPM](https://nodei.co/npm/generator-api.png?downloads=true)](https://nodei.co/npm/generator-api/)

Yeoman generator for creating RESTful NodeJS APIs, using ES6, Mongoose and Express. The fastest way to get your project up and running using an awesome stack.

![generator](http://yeoman.io/static/illustration-home-inverted.91b07808be.png)


## Getting started

- Make sure you have [yeoman](https://github.com/yeoman/yo) installed on your machine:
    `npm install -g yo`
- Install the generator **globally**: `npm install -g generator-api`
- Run: `yo api`, or `yo` and choose `Api` option

## Running the generated project

Make sure you have node version `>= 6` because this project uses native supported ES6 features.

### Development

- Run: `mongod` to start the local mongodb in a separated terminal instance (If you don't have mongodb installed locally, visit It's [webpage](https://docs.mongodb.com/manual/installation/) to learn how to install it).
- Run: `npm run dev` to run the app (By default the app will run at `localhost:8080`, you can change this in the config file).

**Did you choose Docker support?** :whale:

You only need [Docker](https://docs.docker.com/engine/installation/) and [docker-compose](https://docs.docker.com/compose/install/) installed, no mongodb, no node, no npm. :sunglasses:

- Run: `docker-compose up` to run the app. _You might need `sudo` for this one_.

### Production

You'll likely be consuming mongodb as a service, so make sure to set the env var pointing at it.

Just run `npm start`.

**Wait, you choose Docker right?** :whale:

Build the Docker container and run it:

```bash
sudo docker build -t <image-name> .
sudo docker run \
  -p <host-port>:8080 \
  -d <image-name> \
  -e MONGO_DB_URI=mongodb://<username>:<password>@<host>:<port> \
  npm run start
```

## Architecture
The idea is to be able to scale having a simple architecture. Assuming we use `user` and `pet` as models the generated project would look like this:

```
├───index.js
├───routes.js
├───package.json
├───config.js
└───lib/
|   ├───controller.js
|   ├───facade.js
└───model/
    ├───user/
    │   └───user-controller.js
    |   └───user-facade.js
    |   └───user-router.js
    |   └───user-schema.js
    └───pet/
        └───pet-controller.js
        └───pet-facade.js
        └───pet-router.js
        └───pet-schema.js
```

#### Controller:
HTTP layer, in this instance you can manage express request, response and next. In `lib/controller` are the basic RESTful methods `find`, `findOne`, `findById`, `create`, `update` and `remove`. Because this class is extending from there, you got that solved. You can overwrite extended methods or create custom ones here.

#### Facade:
This layer works as a simplified interface of mongoose and as Business Model layer, in this instance you can manage your business logic. For example, if you want to create a pet before creating a user, because you'll end up adding that pet to the person, this is the place.

In `lib/facade` you have the basic support for RESTful methods. Because this class is extending from there, you got that solved. You can overwrite extended methods or create custom ones here. Also you can support more mongoose functionality like `skip`, `sort` etc.


## To do
* Create more generator templates to add new models once the project was initialized
* Implement testing in the generated project

## Contributing
Contributors are welcome, please fork and send pull requests! If you have any ideas on how to improve this project please submit an issue.


## License
[MIT License](https://github.com/ndelvalle/generator-api/blob/master/LICENSE)
