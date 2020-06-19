<template>
  <div class="columns">
    <div class="column is-three-fifths is-offset-one-fifth">
      <a
        href="employee/add"
        class="button is-primary is-pulled-right"
        style="margin: 20px 0;"
      >
        Add Employee
      </a>
      <vuetable
        ref="vuetable"
        :fields="['employee_name', 'employee_salary', 'employee_age', 'action']"
        :css="table"
        :api-url="baseApi"
      >
        <div slot="employee_salary" slot-scope="props">
          Rp{{
            props.rowData.employee_salary
              .toString()
              .replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1.')
          }}
        </div>
        <div slot="action" slot-scope="props">
          <a :href="`employee/${props.rowData.id}`">Detail</a>
          <a :href="`employee/edit/${props.rowData.id}`">Edit</a>
          <a :href="`employee/delete/${props.rowData.id}`">Delete</a>
        </div>
      </vuetable>
    </div>
  </div>
</template>

<script>
import Vuetable from 'vuetable-2'

export default {
  components: {
    Vuetable
  },
  data() {
    return {
      baseApi: process.env.BASE_API,
      table: {
        tableWrapper: '',
        tableHeaderClass: 'fixed',
        tableBodyClass: 'vuetable-semantic-no-top fixed',
        tableClass: 'table is-fullwidth is-striped',
        loadingClass: 'loading',
        ascendingIcon: 'blue chevron up icon',
        descendingIcon: 'blue chevron down icon',
        ascendingClass: 'sorted-asc',
        descendingClass: 'sorted-desc',
        sortableIcon: 'grey sort icon',
        handleIcon: 'grey sidebar icon'
      }
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
