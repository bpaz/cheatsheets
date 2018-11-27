---
title: Axios
layout: 2017/sheet
category: JavaScript libraries
intro: "Promise based HTTP client for the browser and node.js"
---

## Configuration

### Creating an axios instance

```js
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```

### Override defaults

```js
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

## Requests

### GET Request

```js
const response = await axios.get('/user?ID=12345');
  ```

### POST Request

```js
const response = await = axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
```

## Reference

* [Axios Reference](https://github.com/axios/axios)