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
- ketika menginstall nuxt js jangan lupa sertakan axios untuk integrasi API nya

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

## 2. Integration Datatable
1. Install vuetable-2 package di project anda
- instal `npm install vuetable-2@next --save`
2. Cara install vuetable-2 di component
- import vuetable anda dengan cara tambahkan script berikut didalam tag script `import Vuetable from 'vuetable-2'`
- kemudian tambahan `components` di dalam script `export default` dengan nama `Vuetable`
- kurang lebih seperti berikut tambahan filenya
```
<script>
import Vuetable from 'vuetable-2'

export default {
  components: {
    Vuetable
  },
  .......
```
3. Contoh cara penggunaan vuetable-2
```
<vuetable
  ref="vuetable"
  :fields="['employee_name', 'employee_salary', 'employee_age', 'action']"
  :css="table"
  api-url="http://dummy.restapiexample.com/api/v1/employees"
></vutable>
```
- :fields = nama field yang digunakan
- :css    = jika mau mengcustom tampilan table
- api-url = alamat api GET

## 3. Integrasi Create Form
1. Buat form dengan 3 inputan field (name, salary, age).
2. Siapkan satu object variable untuk menampung data requestData, contoh:
```
const requestData = {
  name: this.name,
  salary: this.salary,
  age: this.age
}
```
3. Buat satu API POST untuk mengirim data ke server.
```
await this.$axios
  .$post(`alamat_url_post`, requestData)
  .then(function() {
    window.location = '/'
  })
  .catch((error) => {
    console.log(error)
  })
```
- `then` berfungsi jika API yang di request berhasil
- `catch` berfunsi jika API yand di request gagal

Resource:
Free API : http://dummy.restapiexample.com/
