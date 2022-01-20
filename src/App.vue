<template>
  <div id="app">
    <div class="nav">
      <h1><strong class="nav-title">tk</strong>ambio</h1>
    </div>

    <h2 class="subtitle">Generador de reportes TK</h2>

    <Table></Table>

    <a href="#" id="show-modal" @click="showModal = true" class="btn">Crear Reporte</a>


    <!-- Modal -->
    <modal v-if="showModal" @close="showModal = false"></modal>
  </div>
</template>

<script>
import Table from './components/Table.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    Modal,
    Table
  },
  data() {
    return {
      showModal: false
    }
  },
}
</script>

<style lang="scss" >
.nav {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 20px 0px;

  position: absolute;
  width: 100%;
  height: 74px;
  left: 0px;
  top: 0px;

  background: linear-gradient(180deg, #02ADF1 -2.37%, #4562E6 124.84%, #4563E6 124.84%);
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);

  &-title {
    color: #FFBE12;
  }
}

.subtitle {
  margin: 9rem 0rem 4rem 0rem;
  width: 100%;
}

.btn {
  margin-top: 2rem;
  display: inline-block;
  padding: 12px 40px;
  background: #FFBE12;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 50px;
  text-decoration: none;
  color: #181818;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h3 {
  color: #181818 !important;
}

</style>
