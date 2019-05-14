<img src="https://res.cloudinary.com/adonisjs/image/upload/q_100/v1557762307/poppinss_iftxlt.jpg" max-width="600px">

# Response
[![circleci-image]][circleci-url] [![npm-image]][npm-url] ![](https://img.shields.io/badge/Typescript-294E80.svg?style=for-the-badge&logo=typescript)

Wrapper over NodeJs [res](https://nodejs.org/dist/latest/docs/api/http.html#http_class_http_serverresponse) object to simplify the process of sending HTTP response.

## Features
1. Simple to use API for making HTTP response.
2. Properly closes the streams `pipe` to the response object.
3. Support for lazily sending the response. Helpful when you want to mutate the response inside a `downstream middleware`.
4. Etag generation.
5. In built support for sending plain and signed cookies.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of contents

- [Usage](#usage)
- [Usage](#usage-1)
- [Config](#config)
- [API](#api)
- [AdonisJs usage](#adonisjs-usage)
- [Change log](#change-log)
- [Contributing](#contributing)
- [Authors & License](#authors--license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Usage
## Usage
Install the package from npm as follows:

```sh
npm i @poppinss/response

# yarn
yarn add @poppinss/response
```

and then use it as follows

```ts
import { Response, ResponseConfigContract } from '@poppinss/response'
import { createServer } from 'http'

const config: ResponseConfigContract = {
  etag: false,
  jsonpCallbackName: 'callback',
  secret: 'optional-secret-to-sign-cookies',
  cookie: {},
}

createServer((req, res) => {
  const response = new Response(req, res, config)

  response.send({ hello: 'world' }) // objects
  response.send(Buffer.from('hello world')) // buffer
  response.send(true) // boolean
  response.send(10) // numbers
  response.send('<p> Hello world </p>') // html

  response.pipe(fs.createReadStream('profile.jpg')) // streams
  response.download('path/to/file.jpg') // stream files
  response.attachment('path/to/file.jpg') // set Content-Disposition header

  response.cookie('session-id', '1') // set signed cookie
})
```

## Config
<table>
  <tr>
    <td colspan="2"><code>{</code></td>
  </tr>
  <tr>
    <td valign="top"><code>"etag": false</code></td>
    <td>
      <p>
      Whether or not to generate <code>etag</code> for all responses. Etag helps the browser for re-using the cache response when etags are same.
      Default value is <code>false</code>
      </p>
    </td>
  </tr>
  <tr>
    <td valign="top"><code>"jsonpCallbackName": "callback"</code></td>
    <td>
      <p>
      The callback name for the JSONP response. In case of dynamic callback names, you can passing it inline when calling <code>response.jsonp()</code> method.
      </p>
    </td>
  </tr>
  <tr>
    <td valign="top"><code>"secret"</code></td>
    <td>
      <p>
        <strong>Optional</strong> Define a secret to sign cookies. </p>
    </td>
  </tr>
  <tr>
    <td valign="top"><code>"cookie"</code></td>
    <td>
      <p>
      <strong>Partial</strong> Config to generate the cookie header. Make sure to check <a href="https://www.npmjs.com/package/cookie">cookie</a> package docs for list of available options.
      </p>
    </td>
  </tr>
  <tr>
    <td colspan="2"><code>}</code></td>
  </tr>
</table>

## API
Following are the autogenerated files via Typedoc

* [API](docs/README.md)

## AdonisJs usage
AdonisJs leverages the IoC container for resolving dependencies, which means you cannot import modules from the filesystem directly and must always rely on the resolution logic of the container.

Now since the IOC container computes the output value at runtime, it's impossible for Typescript to provide intellisense for same. To encouter this problem, we export `an ambient module` that you can use for typehinting as follows.

```ts
import { Response } from '@ioc:Adonis/Src/Response'
const response = new Response(req, res, config)
```

## Change log

The change log can be found in the [CHANGELOG.md](CHANGELOG.md) file.

## Contributing

Everyone is welcome to contribute. Please go through the following guides, before getting started.

1. [Contributing](https://adonisjs.com/contributing)
2. [Code of conduct](https://adonisjs.com/code-of-conduct)


## Authors & License
[Harminder virk](https://github.com/Harminder virk) and [contributors](https://github.com/poppinss/response/graphs/contributors).

MIT License, see the included [MIT](LICENSE.md) file.

[circleci-image]: https://img.shields.io/circleci/project/github/poppinss/response/master.svg?style=for-the-badge&logo=circleci
[circleci-url]: https://circleci.com/gh/poppinss/response "circleci"

[npm-image]: https://img.shields.io/npm/v/@poppinss/response.svg?style=for-the-badge&logo=npm
[npm-url]: https://npmjs.org/package/@poppinss/response "npm"
