-<template>
  <div class="columns">
    <div class="column is-half is-offset-one-quarter">
      <form @submit="submitAdd">
        <div class="field">
          <label class="label">Employee Name</label>
          <div class="control">
            <input
              v-model="name"
              class="input"
              type="text"
              placeholder="please input employee name"
            />
          </div>
        </div>
        <div class="field">
          <label class="label">Employee Salary</label>
          <div class="field-body">
            <div class="field is-expanded">
              <div class="field has-addons">
                <p class="control">
                  <a class="button is-static">
                    Rp
                  </a>
                </p>
                <p class="control is-expanded">
                  <input
                    v-model="salary"
                    class="input"
                    type="number"
                    placeholder="Your phone number"
                  />
                </p>
              </div>
              <p class="help">Do not enter the first zero</p>
            </div>
          </div>
        </div>
        <div class="field">
          <label class="label">Age</label>
          <div class="control">
            <input
              v-model="age"
              class="input"
              type="number"
              placeholder="please input age"
            />
          </div>
        </div>
        <button class="button is-primary is-pulled-right">Save</button>
      </form>
    </div>
  </div>
</template>

<script>
// import swal from 'vue-sweetalert2'

export default {
  data() {
    return {
      baseApi: process.env.BASE_API,
      name: '',
      salary: 0,
      age: 0
    }
  },
  methods: {
    async submitAdd(e) {
      e.preventDefault()

      const requestData = {
        name: this.name,
        salary: this.salary,
        age: this.age
      }
      await this.$axios
        .$post(`${this.baseApi}Create`, requestData)
        .then((data) => {
          alert('Data Berhasil disimpan!')
          window.location = '/'
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>
