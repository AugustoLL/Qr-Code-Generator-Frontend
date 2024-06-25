# QR Code Generator Frontend
![Vue.js Version](https://img.shields.io/badge/vue-v20.11.0-green?style=for-the-badge&logo=vue.js&labelColor=%232b2b2d)
![Vuetify Version](https://img.shields.io/badge/v3.5.8-js?style=for-the-badge&logo=vuetify&label=vuetify&color=%231867c0)
[![axios Version](https://img.shields.io/badge/axios-v1.7.2-blue?style=for-the-badge&logo=axios)](https://www.npmjs.com/package/axios/v/1.7.2)
![Vite](https://img.shields.io/badge/v5.1.5-js?style=for-the-badge&logo=vite&label=Vite&color=%23a54ffe)


This is a simple Vue.js application for generating QR codes with customizable options.

## ❗️ Features

- Generate QR codes with the following customizable options:
- - URL to encode
- - Image format (PNG, JPEG, WebP)
- - Size
- - Error correction level
- - Dark and light colors
  - Logo overlay with customizable size ratio
- Preview of the QR code generated based on user inputs.

## 💿 Install

1. Clone the repository:
```sh
git clone https://github.com/your-username/qr-code-generator-frontend.git
cd qr-code-generator-frontend
```

2. Install dependencies:
```sh
npm install
```

3. Build and preview:
```sh
npm run build
...
npm run preview
```
The app will be served at localhost:3000 by default.

## ✨ Features

- 🖼️ **Optimized Front-End Stack**: Leverage the latest Vue 3 and Vuetify 3 for a modern, reactive UI development experience. [Vue 3](https://v3.vuejs.org/) | [Vuetify 3](https://vuetifyjs.com/en/)
- 🗃️ **State Management**: Integrated with [Pinia](https://pinia.vuejs.org/), the intuitive, modular state management solution for Vue.
- 🚦 **Routing and Layouts**: Utilizes Vue Router for SPA navigation and vite-plugin-vue-layouts for organizing Vue file layouts. [Vue Router](https://router.vuejs.org/) | [vite-plugin-vue-layouts](https://github.com/JohnCampionJr/vite-plugin-vue-layouts)
- 💻 **Enhanced Development Experience**: Benefit from TypeScript's static type checking and the ESLint plugin suite for Vue, ensuring code quality and consistency. [TypeScript](https://www.typescriptlang.org/) | [ESLint Plugin Vue](https://eslint.vuejs.org/)
- ⚡ **Next-Gen Tooling**: Powered by Vite, experience fast cold starts and instant HMR (Hot Module Replacement). [Vite](https://vitejs.dev/)
- 🧩 **Automated Component Importing**: Streamline your workflow with unplugin-vue-components, automatically importing components as you use them. [unplugin-vue-components](https://github.com/antfu/unplugin-vue-components)
- 🛠️ **Strongly-Typed Vue**: Use vue-tsc for type-checking your Vue components, and enjoy a robust development experience. [vue-tsc](https://github.com/johnsoncodehk/volar/tree/master/packages/vue-tsc)

These features are curated to provide a seamless development experience from setup to deployment, ensuring that your Vuetify application is both powerful and maintainable.

## 💡 Usage

1. Open your browser and navigate to the application URL.
2. Enter the URL you want to encode.
3. Customize the QR code appearance:
  - Select image format (PNG, JPEG, WebP).
  - Choose the size of the QR code.
  - Pick colors for the pattern and background.
  - Optionally, provide a logo URL and adjust the size ratio.
  - The preview will update dynamically based on your selections.
4. Click "Generate" to see the final QR code image.

## 🖼️ Examples


Technologies Used

- Vue.js
- Vite
- Vuetify
- Axios


## 📑 License
[MIT](http://opensource.org/licenses/MIT)

This project is licensed under the MIT License.
