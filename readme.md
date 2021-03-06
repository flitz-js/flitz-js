# flitz

Welcome to [flitz](https://github.com/flitz-js/flitz) [[**ˈflɪt͡s**](https://en.wikipedia.org/wiki/Naming_conventions_of_the_International_Phonetic_Alphabet)], a lightweight and extremly fast HTTP server with all basics for [Node 10+](https://nodejs.org/docs/latest-v10.x/api/http.html), written in [TypeScript](https://www.typescriptlang.org/).

To install *flitz*, simply run

```bash
npm install --save flitz
```

from the folder, where your `package.json` file is stored and start with some like that:

```javascript
const flitz = require('flitz');

const run = async () => {
  const app = flitz();

  app.get('/', async (req, res) => {
    res.write('Hello world!');
    res.end();
  });

  await app.listen(3000);
};

run();
```

Or the TypeScript way:

```typescript
import flitz from 'flitz';

const run = async () => {
  const app = flitz();

  app.get('/', async (req, res) => {
    res.write('Hello world!');
    res.end();
  });

  await app.listen(3000);
};

run();
```

## Middlewares

You can also define middlewares for each of your routes:

```typescript
import flitz from 'flitz';
// s. https://github.com/flitz-js/body
import { body } from '@flitz/body';

const run = async () => {
  const app = flitz();

  //             👇👇👇
  app.post('/', [ body() ], async (req, res) => {
    const body = req.body as Buffer;

    res.write('Your body as string: ' + body.toString('utf8'));
    res.end();
  });

  await app.listen(3000);
};

run();
```

## Useful modules

| Name | Description |
|---|---|
| [accept-language](https://github.com/flitz-js/accept-language) | Extracts data from [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) request header field and makes it available in a [flitz](https://github.com/flitz-js/flitz) request. |
| [body](https://github.com/flitz-js/body) | Reads and/or parses the request body and makes the data available in `body` property of the request object of the underlying handler. |
| [cookies](https://github.com/flitz-js/cookies) | Extracts cookies and makes the data available in `cookies` property of the request object of the underlying handler. |
| [errors](https://github.com/flitz-js/errors) | Pretty error handling. |
| [params](https://github.com/flitz-js/params) | Extracts path parameters and makes the data available in `params` property of the request object of the underlying handler. |
| [swagger](https://github.com/flitz-js/swagger) | Sets up a [Swagger UI](https://github.com/swagger-api/swagger-ui) for a flitz instance. |
