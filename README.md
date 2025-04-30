# Visit

I’ve deployed the app to Vercel: https://vue-weather-liart.vercel.app

You’re also welcome to run it locally:

```bash
pnpm i
pnpm dev # or: pnpm run dev
```

# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

Learn more about IDE Support for Vue in the [Vue Docs Scaling up Guide](https://vuejs.org/guide/scaling-up/tooling.html#ide-support).

# Start

```bash
pnpm i
pnpm dev # or pnpm run dev
```

<!-- # Refresh Data Triggers -->

1. When switching tabs
2. When pulling down to refresh the page

# Todo

There’s still no AJAX call in the code.
The API doesn’t seem to work—possibly due to an issue with the appid.
Example request:
https://api.openweathermap.org/data/3.0/onecall?lat=33.44&lon=-94.04&appid=9170e0e85794088df319259526c55afd

# Steps to create the application

```bash
pnpm create vite@latest vue-weather --template vue
cd vue-weather
pnpm i
pnpm dev # or: pnpm run dev

pnpm add tailwindcss @tailwindcss/vite # then import tailwindcss and add plugins in vite.config.js

pnpm add element-plus @element-plus/icons-vue # UI library

```
