<template>
    <div class="content-table">
        <div class="table">
            <div class="table-head">
                <span style="padding-bottom: 10px">Titulo</span>
                <span style="padding-bottom: 10px">Fecha de creación</span>
                <span style="padding-bottom: 10px">Acción</span>
            </div>

            <div class="table-body">
                <p>Reporte 1</p>
                <p style="width: 5px; background: #C4C4C4"></p>
                <p>26/08/2022</p>
                <p style="width: 5px; background: #C4C4C4"></p>
                <p>
                    <a href="#" target="_blank">Decargar
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-download" viewBox="0 0 16 16">
                          <path d="M.5 9.9a.5.5 0 0 1 .5.5v2.5a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1v-2.5a.5.5 0 0 1 1 0v2.5a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2v-2.5a.5.5 0 0 1 .5-.5z"/>
                          <path d="M7.646 11.854a.5.5 0 0 0 .708 0l3-3a.5.5 0 0 0-.708-.708L8.5 10.293V1.5a.5.5 0 0 0-1 0v8.793L5.354 8.146a.5.5 0 1 0-.708.708l3 3z"/>
                        </svg>
                    </a>
                </p>
            </div>
            <div class="table-body">
                <p>Reporte 2</p>
                <p style="width: 5px; background: #C4C4C4"></p>
                <p>26/08/2021</p>
                <p style="width: 5px; background: #C4C4C4"></p>
                <p>
                    <a href="#" target="_blank">Decargar
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-download" viewBox="0 0 16 16">
                          <path d="M.5 9.9a.5.5 0 0 1 .5.5v2.5a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1v-2.5a.5.5 0 0 1 1 0v2.5a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2v-2.5a.5.5 0 0 1 .5-.5z"/>
                          <path d="M7.646 11.854a.5.5 0 0 0 .708 0l3-3a.5.5 0 0 0-.708-.708L8.5 10.293V1.5a.5.5 0 0 0-1 0v8.793L5.354 8.146a.5.5 0 1 0-.708.708l3 3z"/>
                        </svg>
                    </a>
                </p>
            </div>
            <div class="table-body">
                <p>Reporte 3</p>
                <p style="width: 5px; background: #C4C4C4"></p>
                <p>26/08/2020</p>
                <p style="width: 5px; background: #C4C4C4"></p>
                <p>
                    <a href="#" target="_blank">Decargar
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-download" viewBox="0 0 16 16">
                          <path d="M.5 9.9a.5.5 0 0 1 .5.5v2.5a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1v-2.5a.5.5 0 0 1 1 0v2.5a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2v-2.5a.5.5 0 0 1 .5-.5z"/>
                          <path d="M7.646 11.854a.5.5 0 0 0 .708 0l3-3a.5.5 0 0 0-.708-.708L8.5 10.293V1.5a.5.5 0 0 0-1 0v8.793L5.354 8.146a.5.5 0 1 0-.708.708l3 3z"/>
                        </svg>
                    </a>
                </p>
            </div>

<!--             <div class="table-body" v-for="(item, index) in reports" :key="index">
                <p>{{ item.title }}</p>
                <p style="width: 5px; background: #C4C4C4"></p>
                <p>{{ item.created_at }}</p>
                <p style="width: 5px; background: #C4C4C4"></p>
                <p><a :href="`http://apitkambio.test${item.report_link}`" target="_blank">Decargar</a></p>
            </div> -->
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
        //this.getReports()
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

  padding: 10px 30px 40px;

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

.content-table {
  margin-left: auto;
  margin-right: auto;
  width: 70%;
}

@media (max-width: 767px) {
.content-table {
  width: 100%;
  }
}
</style>
