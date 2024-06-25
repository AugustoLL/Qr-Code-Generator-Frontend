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

3. Start the development server:
```sh
npm run dev
```

3. OR Build and preview:
```sh
npm run build
...
npm run preview
```

The app will be served at localhost:3000 by default.

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

<img src="examples/example1.png" />
<img src="examples/example2.png" />


Technologies Used

- Vue.js
- Vite
- Vuetify
- Axios


## 📑 License
[MIT](http://opensource.org/licenses/MIT)

This project is licensed under the MIT License.
