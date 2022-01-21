<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
            <slot name="header">
              <h3>Reporte por fecha de nacimiento</h3>
              <p class="title-dos">Ingresa los siguientes datos para generar tu reporte</p>
            </slot>
          </div>

          <form @submit.prevent="submit">
            <div class="modal-body">
              <slot name="body">
                <fieldset>
                  <legend>Descripción del reporte</legend>
                  <input type="text" v-model="title" placeholder="Descripción">
                </fieldset>
                <span class="text-middle">Fecha de nacimiento</span>
                <div class="dates">
                  <fieldset class="fieldsett">
                    <legend>Inicio</legend>
                    <input type="date" v-model="startDate">
                  </fieldset>

                  <fieldset class="fieldsettt">
                    <legend>Fin</legend>
                    <input type="date" v-model="lastDate">
                  </fieldset>

                </div>
              </slot>
            </div>

            <div class="modal-footer">
<!--               <slot name="footer">
                default footer
                <button class="modal-default-button" @click="$emit('close')">
                  OK
                </button>
              </slot> -->
              <button class="btn" @click="$emit('close')">Generar reporte</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import axios from "axios";

export default {
  name: 'Modal',
  data() {
    return {
      title: '',
      startDate: '',
      lastDate: '',
    }
  },
  methods: {
    submit() {
      console.log(this.startDate);
      axios.get('http://apitkambio.test/api/generate-report', {
          responseType: 'blob',
          params: {
            startDate: this.startDate,
            lastDate: this.lastDate,
            title: this.title
          }
        })
        .then(response => {
          console.log(response.data);
          const url = URL.createObjectURL(new Blob([response.data]))
          const link = document.createElement('a')
          link.href = url
          link.setAttribute(
            'download',
            `${new Date().toLocaleDateString()}.xlsx`
          )
          document.body.appendChild(link)
          link.click()
        })
        .catch(function (error) {
          console.log(error);
        })
        .then(function () {
          // always executed
        });


    },
  }
}
</script>

<style lang="scss" >
.fieldsett {
    border: 1px solid #B1B1B1;
    border-radius: 6px;
    width: 50%;
}
.fieldsettt {
    border: 1px solid #B1B1B1;
    border-radius: 6px;
    width: 50%;
}
.dates {
    display: flex;
}
span.text-middle {
    font-size: smaller;
    color: #696969;
    padding: 15px 0px;
    display: block;
    position: relative;
}
.title-dos {
  color: #565656;
  font-size: small;
  margin-bottom: 2rem;
}
input[type="text"] {
    border: white;
    font-size: smaller;
    color: #696969;

}
input[type="date"] {
    border: white;
    font-size: smaller;
    color: #696969;
    width: -webkit-fill-available;
}
legend {
  display: block;
  padding-left: 2px;
  padding-right: 2px;
  border: none;
  font-size: smaller;
}
fieldset {
  border: 1px solid #B1B1B1;
  border-radius: 6px;
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 35%;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
  border-radius: 6px;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
  text-align: initial;
}

.modal-default-button {
  float: right;
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

@media (max-width: 1024px) {

  .dates {
      display: block;
  }
  .fieldsett {
      border: 1px solid #B1B1B1;
      border-radius: 6px;
      width: 90%;
  }
  .fieldsettt {
      border: 1px solid #B1B1B1;
      border-radius: 6px;
      width: 90%;
      margin-top: 1rem;
  }
}

@media (max-width: 425px) {
.modal-container {
  width: 80%;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
  border-radius: 6px;
}
}
</style>
