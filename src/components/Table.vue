<template>
    <div class="table">
        <div class="table-head">
            <span style="padding-bottom: 10px">Titulo</span>
            <span style="padding-bottom: 10px">Fecha de creación</span>
            <span style="padding-bottom: 10px">Acción</span>
        </div>

        <div class="table-body" v-for="(item, index) in reports" :key="index">
            <p>{{ item.title }}</p>
            <p style="width: 5px; background: #C4C4C4"></p>
            <p>{{ item.created_at }}</p>
            <p style="width: 5px; background: #C4C4C4"></p>
            <p><a :href="`http://apitkambio.test${item.report_link}`" target="_blank">Decargar</a></p>
        </div>
    </div>
</template>

<script>
import axios from "axios"

export default {
    name: 'Table',
    data() {
        return {
            reports: [],
        }
    },
    created() {
        this.getReports()
    },
    methods: {
        getReports() {
            axios.get('http://apitkambio.test/api/list-reports')
            .then(response => {
                this.reports = response.data;
            })
            .catch(error => {
                console.log(error);
            })
        },
    }
}
</script>

<style lang="scss" >
a {
    text-decoration: none;
    color: #FFFFFF;
}
.table {
  margin-left: auto;
  margin-right: auto;
  padding: 10px 30px 40px;

  width: 690px;
  height: 212px;
  left: 0px;
  top: 0px;

  background: #4563E6;
  border-radius: 10px;

  &-head {
    display: flex;
    justify-content: space-between;
    color: #FFFFFF;
    border-bottom: 5px solid #C4C4C4
  }

  &-body {
    display: flex;
    justify-content: space-between;
    color: #FFFFFF;
    border-bottom: 2px solid #C4C4C4;
    flex-direction: row;
  }

  &-body:last-child {
    border-bottom: 0px solid red !important;
  }

}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}


</style>
