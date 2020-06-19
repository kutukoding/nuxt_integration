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
- jika ingin mengikuti step by step lihat branch sesuai urutan angka nya

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

## 4. Integrasi Detail
1. Copy form dari add dan beri nama file `_id.vue`
2. tambahkan fungsi di `methods`:
```
async getDetail() {
  const { id } = this.$route.params
  const thisVue = this
  await this.$axios
    .$get(`url_get/${id}`)
    .then((result) => {
      thisVue.name = result.employee_name
      thisVue.salary = result.employee_salary
      thisVue.age = result.employee_age
    })
    .catch((error) => {
      console.log('error:', error)
    })
}
```
- `id` berfungsi mengambil id dari url
- `$axios.$get(url)` befungsi mengambil data dari API dengan memberikan syarat id
3. Panggil fungsi tersebut kedalam `mounted` agar dijalankan pertama kali

## 5. Integrasi Update
1. Copy form dari add dan buat folder dengan nama `edit` dan buat 1 file didalam folder tersebut dengan nama file `_id.vue`
2. rubah fungsi submit formnya ke fungsi update:
```
async submitEdit(e) {
  e.preventDefault()

  const requestData = {
    name: this.name,
    salary: this.salary,
    age: this.age
  }
  await this.$axios
    .$put(`alamat_update/id`, requestData)
    .then((data) => {
      alert('Data Berhasil disimpan!')
      window.location = '/'
    })
    .catch((error) => {
      console.log(error)
    })
}
```
- berbeda dengan detail maupun update, jika update menggunakan fungsi `$put`
- dengan mengirimkan alamat update beserta id yang akan dirubah, dan mengirimkan `requestData`

## 6. Integrasi Delete
1. buat fungsi untuk delete seperti berikut:
```
async employeeDelete(id) {
  if (confirm('Are you sure delete this employee?')) {
    await this.$axios
      .$delete(`alamat_delete/id`, {
        data: {
          _id: id
        }
      })
      .then((result) => {
        alert('Data berhasil dihapus!')
      })
      .catch((error) => {
        console.log('error:', error)
      })
  }
}
```
- `confirm()` membuat konfirmasi dari alert
- `.$delete(alamat_delete/id, requestBody)` masukan alamat_delete dan id yang sesuai, jika memerlukan requestBody maka tambahkan seperti contoh diatas 

Resource:
API : https://almock.alterra.dev/enhydra/
