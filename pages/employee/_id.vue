<template>
  <div class="columns">
    <div class="column is-half is-offset-one-quarter">
      <form>
        <div class="field">
          <label class="label">Employee Name</label>
          <div class="control">
            <input
              v-model="name"
              readonly
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
                    readonly
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
              readonly
              class="input"
              type="number"
              placeholder="please input age"
            />
          </div>
        </div>
        <router-link to="/" class="button is-secondary is-pulled-left">
          Back
        </router-link>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      baseApi: process.env.BASE_API,
      name: '',
      salary: 0,
      age: 0
    }
  },
  mounted() {
    this.getDetail()
  },
  methods: {
    async getDetail() {
      const { id } = this.$route.params
      const thisVue = this
      await this.$axios
        .$get(`${this.baseApi}/${id}`)
        .then((result) => {
          thisVue.name = result.employee_name
          thisVue.salary = result.employee_salary
          thisVue.age = result.employee_age
        })
        .catch((error) => {
          console.log('error:', error)
        })
    }
  }
}
</script>
