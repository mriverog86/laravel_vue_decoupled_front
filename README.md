# Laravel 11 + Vue 3: Vue 3 Single Page App
Example of a decoupled integration between Laravel and a Vue application packed with Vite. This is the frontend component of the system in the form of a Single Page Web Application developed using Vue and packed with Vite.

### Installation Guide

1. Clone the repository to your workspace:

```shell
git clone https://github.com/mriverog86/laravel_vue_decoupled_front.git
```

2. Move inside the project folder:

```shell
cd laravel_vue_decoupled_front
```

3. Install the project dependencies:

```shell
npm install
```

4. Start Vue development server:

```shell
npm run dev
```

## Integration Guide

1. The first step is to create a new Vue project.
```sh
npm create vite@latest
```

2. Install project dependencies.

```bash
npm install
```

3. Install router and axios

```bash
npm install vue-router@4 axios
```

4.  Integrate the router with the Vue instance inside `./src/main.ts` file:

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

const app = createApp(App)

app.use(router)
app.mount("#app");
```

5.  Create `./src/views/HomeView.vue` with a router-link to test internal navigation:

```html
<template>
    <div>
        <h1>HOME</h1>
        <router-link to="/test"> Take me to Test page </router-link>
    </div>
</template>
```

6. Create `./src/views/TestView.vue`

```html
<template>
    <h1>Just a test page!</h1>
</template>
```

7. Next, Lazy load the new route components in the router’s file `./src/router/index.ts`

```javascript
import { createRouter, createWebHistory } from 'vue-router'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: "/",
      name: 'home',
      component: () => import("../views/HomeView.vue"),
    },
    {
        path: "/test",
        name: 'test',
        component: () => import("../views/TestView.vue"),
    },
  ]
})

export default router
```

8.  Modify the Vue entry file to make it dynamic. Vue Router provides RouterView built-in component, which exposes slots that can be used to dynamically render route components. Go to `./src/App.vue` and modify it as follows:

```jsx
<template>
  <router-view v-slot="{ Component, route }">
      <div :key="route.name">
          <Component :is="Component" />
      </div>
  </router-view>
</template>
```

9.  Consume Laravel backend `./test-me` API endpoint from `./src/views/HomeView.vue` component using axios. Let’s prepare a button that will get the response.

```html
<template>
    <div>
        <h1>HOME</h1>
        <router-link to="/test"> Take me to Test page </router-link>
        <button @click.prevent="tiggerEndpoint">Trigger Endpoint</button>
        <p v-if="response">{{ response.data }}</p>
    </div>
</template>
```

10. Setting up an environment variable in `.env` to stablish the Laravel API base url:
```yml
VITE_API_BASE_URL=http://127.0.0.1:8000
```

11. Finally, add the script setup to create the function and variable ref in `./src/views/HomeView.vue`.

```javascript
<script setup>
import axios from "axios";
import { ref } from "vue";

const response = ref();

const getValue = async () => {
    try {
        response.value = await axios.get(import.meta.env.VITE_API_BASE_URL + "/api/test-me");
    } catch (error) {
        // Do something with the error
        console.log(error);
    }
};
</script>
```

## Recomentations

You can send any recomendations to [mriverog86@gmail.com](mailto:mriverog86@gmail.com).