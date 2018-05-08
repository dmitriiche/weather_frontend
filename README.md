# weather frontend demo app
Minimal vue demo project.
The app send a GET requests to the REST api. And display daily weather and 5 days forecasts.

## Requirements
- [NodeJs v9.9.0](https://nodejs.org/en/download/)
- [Vue 2.5.16](https://vuejs.org/v2/guide/installation.html)

## Running the application locally
- Go to the project directory
- Install npm dependencies

```shell
npm install
```
- Run dev server

```shell
npm run dev
```

Server start at the localhost:8080


Backend server URL can be changed by edit main.js "Vue.http.options.root" property.
