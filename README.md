# Laravel 11 + Vue 3: Vue 3 Single Page App
Example of a decoupled integration between Laravel and a Vue application packed with Vite. This is the frontend component of the system in the form of a Single Page Web Application developed using Vue and packed with Vite.

## Main steps

### Creating environment variable:
* Setting up an environment variable in `.env` to stablish the api base url:
```yml
VITE_API_BASE_URL=http://127.0.0.1:8000
```

### Consuming API endpoint:
* Loading the api base url from `.env` and fetching data from api endpoint:
  
```javascript
response.value = await axios.get(import.meta.env.VITE_API_BASE_URL + "/api/test-me");
```

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
