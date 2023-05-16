Spin up a fast API from a CSV or JSON source file.

## Commandline usage (for development)

Install to your project with `npm install --save @livingpixel/lore`

Create a basic CSV file like:

```
city, province, pop. (M)
Toronto, ON, 5.6
Montreal, QC, 3.7
Vancouver, BC, 2.4
```

Start server: `npx lore myfile.csv --key=city`

Visit `http://localhost:3000/` or `http://localhost:3000/Toronto`

## As Express middleware (for production)

```ts
import lore from 'lore';
import path from 'path';
import express from 'express';

const app = express();

app.use('/population-data', lore(path.join(process.cwd(), 'mydata.csv'), {
  key: 'city',
});

app.start();
```

You can use any other middleware for caching, authentication, throttling, and so on.

## Options

Options can be passed either as command-line arguments, or as the second argument passed to the `lore` factory function, as above.

**key** - Primary key used to retrieve data.

**limit** - when a value is provided, limit the results retrieved from the root/list endpoint to the value provided. Additional pages can be returned by specifying a `page` in the query string. 

### Middleware options

These options can only be provided in middleware mode:

**readIn** - when the server starts up, read the file one time and save each row to a database according to the callback provided

**readOut** - callback function to retrieve the given row from the database

**readOutList** - callback function to retrieve the index view from the database

## Roadmap

Streaming option

GraphQL
