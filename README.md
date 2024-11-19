# DemoForm
This template should help get you started developing with Vue 3 in Vite.

### Refer to the VueJs offical documentation(https://vuejs.org/)

### Create a Vue Project using the command
```sh
npm create vue@latest
```
### Setup the following as per the requirement
```sh
✔ Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add an End-to-End Testing Solution? … No / Cypress / Nightwatch / Playwright
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes
✔ Add Vue DevTools 7 extension for debugging? (experimental) … No / Yes
```

### Go to your current project
```sh
cd <your-project-name>
```

### Install dependencies
```sh
npm install
```


### The Project is Setup successfully, now run the command
```sh
npm run dev
```

### To install PrimeVue(similar to bootstrap) run the command to install dependencies
```sh
npm install primevue
```

### Setup main.js as per the steps in PrimeVue Documentation,refer official webiste(https://primevue.org/setup/)

```sh
import './assets/main.css'
import { createApp } from 'vue'
import App from './App.vue'
import PrimeVue from 'primevue/config';
import Aura from '@primevue/themes/aura';


const vueApp = createApp(App).use(PrimeVue, {
    theme: {
        preset: Aura,
        options: {
            darkModeSelector: false,
        }
    }
});
vueApp.mount("#app");
```

### To install PrimeFlex(similar to tailwaind) run the command to install dependencies, refer officil website(https://primeflex.org/installation)
```sh
npm install primefelx
```

### To use icons in the application we can integrate PrimeIcons, using the command, refer official website(https://primeng.org/icons)
```sh
npm install primeicons
```
 
