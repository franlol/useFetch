# useFetch - React custom hook

Hook to fetch data with [fetchAPI](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

Also can handle errors and loading state.

## Why useFetch?

With this hook, you can get a json data from an url and handle the following variables:

- Fetched data.
- Loading boolean.
- Error data.

When that vars are updated, your component is re-rendedred.

## Usage

Just install:

```console
npm install react-hook-usefetch
```

And import the hook.

```javascript
import useFetch from 'react-hook-usefetch';
```

Use it in your component:

```javascript
const YourComponent = props => {
  ...
  const data = useFetch('url', options);
  ...
}
```

Optional, you can send personal settings as second parameter:

```javascript
const headers = new Headers();

const options = {
  method: 'GET',
  headers,
  mode: 'cors',
  cache: 'default',
  ...more
};
```

## Full Example

```javascript
import React from 'react';
import useFetch from 'react-hook-usefetch';

export default () => {
  const { data, loading, error } = useFetch('https://pokeapi.co/api/v2/pokemon', {});

  const getData = () => {
    if (loading) {
      return <p>Loading...</p>;
    }
    if (error.status) {
      return <p>Error: {error.message}</p>;
    }
    if (!data.results) {
      return <p>No data results</p>;
    }
    if (data.results) {
      return data.results.map((poke, i) => <p key={`poke-${i}`}>{poke.name}</p>);
    }
  };

  return (
    <div>
      <h1>Test</h1>
      {getData()}
    </div>
  );
};
```
