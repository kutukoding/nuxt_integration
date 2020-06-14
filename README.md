# nuxt_integration

> basic integration API with nuxt js

## Build Setup

``` bash
# install dependencies
$ npm run install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

------------------------------------------------------------

# Step by Step Integration 

## 1. Setup API
1. Install env package di diproject anda
- install dengan perintah : `yarn add --dev @nuxtjs/dotenv` atau `npm install --save-dev @nuxtjs/dotenv`
  **Note:** jika menggunakan nuxt versi dibawah 2.9 maka tidak perlu menambahkan `--dev` atau `--save-dev`
- kemudian tambahkan di file `nuxt.config.js`
```
  export default {
    buildModules: [
      // Simple usage
      '@nuxtjs/dotenv',
    ]
  }
```
- atau bisa lihat dokumentasinya di : https://github.com/nuxt-community/dotenv-module
2. Masukan link API anda di file `.env` contoh menggunakan api : http://dummy.restapiexample.com/
3. Setelah menyimpan `.env` jangan lupa untuk menjalankan ulang server anda

Resource:
Free API : http://dummy.restapiexample.com/
