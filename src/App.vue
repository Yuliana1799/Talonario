<template>
  <div>
    <div class="contenedor">
      <div class="titulo">
        <h1 class="text_tit">TALONARIO</h1>
      </div>
      <div class="cuerpo">
        <div class="cont1">
          <div class="card1" :style="card1 ? 'display:block' : 'display: none'">
            <div class="info">
              <h1 class="info">INFORMACIÓN</h1>
            </div>
            <div class="cuerpo_info">
              <p>{{ premio }}</p>
            </div>
            <div class="cuerpo_info">
              <p>{{ valor_boleta }}</p>
            </div>
            <div class="cuerpo_info">
              <p>{{ seleccion_loteria }}</p>
            </div>
            <div class="cuerpo_info">
              <p>{{ fecha }}</p>
            </div>
            <div class="cuerpo_info">
              <button class="editar_info" @click="editar_info()">EDITAR</button>
            </div>
          </div>
        </div>
        <div class="cont_2">
          <div class="balotas" v-for="(bola, i) in balotas" :key="i">
            <div class="balota" @click="registrar_balota(i)">
              <p>{{ bola.item }}</p>
            </div>
          </div>
          <div
            class="modal"
            tabindex="-1"
            :style="registro_balota ? 'display:block' : 'display:none'"
          >
            <div class="modal-dialog">
              <div class="modal-content">
                <div class="modal-header">
                  <h5 class="modal-title">Diligenciar la información</h5>
                </div>
                <div class="modal-body">
                  <div class="card1">
                    <div class="cuerpo_info">
                      <p>{{ boletas_adquirir }}</p>
                    </div>
                    <input
                      type="text"
                      value="nombre"
                      placeholder="Nombre"
                      v-model="nombre_persona"
                    />
                    <br />
                    <input
                      type="number"
                      value="telefono"
                      placeholder="Teléfono"
                      v-model="telefono"
                    />
                    <br />
                    <input
                      type="text"
                      value="direccion"
                      placeholder="Direción"
                      v-model="direccion"
                    />
                    <br />
                    <input
                      type="radio"
                      value="Si"
                      name="opcion"
                      v-model="seleccion_pago"
                    />
                    Si
                    <input
                      type="radio"
                      value="No"
                      name="opcion"
                      v-model="seleccion_pago"
                    />
                    No
                  </div>
                </div>
                <div class="modal-footer">
                  <button
                    type="button"
                    class="btn btn-secondary"
                    data-bs-dismiss="modal"
                    @click="registro_balota = false"
                  >
                    Close
                  </button>
                  <button
                    type="button"
                    class="btn btn-primary"
                    @click="agregar()"
                  >
                    Guardar
                  </button>
                </div>
              </div>
            </div>
          </div>

         
        </div>
        <div class="cont3">
           <div class="card1" :style="card1 ? 'display:block' : 'display: none'">
            <div class="info">
              <h1 class="info">INFORMACIÓN</h1>
            </div>
            <div class="cuerpo_info">
              <p>{{ premio }}</p>
            </div>
            <div class="cuerpo_info">
              <p>{{ valor_boleta }}</p>
            </div>
            <div class="cuerpo_info">
              <p>{{ seleccion_loteria }}</p>
            </div>
            <div class="cuerpo_info">
              <p>{{ fecha }}</p>
            </div>
            <div class="cuerpo_info">
              <button class="editar_info" @click="editar_info()">EDITAR</button>
            </div>
          </div>
        </div>
      </div>
      <div
        class="modal"
        tabindex="-1"
        :style="bd ? 'display:block' : 'display:none'"
      >
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Configura tu talonario</h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
                @click="bd = false"
              ></button>
            </div>
            <div class="modal-body">
              <input
                type="number"
                value="premio"
                placeholder="Ingrese el premio"
                v-model="premio"
              />
              <br />

              <input
                type="number"
                value="valor_boleta"
                placeholder="Ingrese el valor de la boleta"
                v-model="valor_boleta"
              />
              <br />
              <label for="#">Seleccione una loteria</label>
              <select v-model="seleccion_loteria">
                <option value="Dorado Mañana">Dorado Mañana</option>
                <option value="Dorado Tarde">Dorado Tarde</option>
                <option value="Santander">Santander</option>
                <option value="Culona">Culona</option>
                <option value="Boyaca">Boyaca</option>
                <option value="Cafeterito">Cafeterito</option>
                <option value="Cundinamarca">Cundinamarca</option>
              </select>
              <br />
              <label for="#">Seleccione el número de puestos</label>
              <select v-model="seleccion_numboletas">
                <option value="0-99">0-99</option>
                <option value="0-999">0-999</option>
                <option value="0-9999">0-9999</option>
              </select>
              <br />

              <input type="date" value="fecha_n" v-model="fecha" />
            </div>

            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                @click="bd = false"
              >
                Cerrar
              </button>
              <button
                type="button"
                class="btn btn-primary"
                @click="crearBalotas()"
              >
                Guardar
              </button>
            </div>
          </div>
        </div>
      </div>
      <footer class="footer">
        <div class="container">
          <span class="text_pie"
            >©Copyright 2024 - Todos los derechos reservados</span
          >
        </div>
      </footer>
    </div>
  </div>
</template>


<script setup>
import { ref } from "vue";
let premio = ref("");
let valor_boleta = ref("");
let seleccion_loteria = ref("");
let fecha = ref("");
let seleccion_numboletas = ref("");
let bd = ref(true);
let registro_balota = ref(false);
let nombre_persona = ref("");
let boletas_adquirir = ref("");
let telefono = ref("");
let direccion = ref("");
let seleccion_pago = ref("");
let card1 = ref(false);
let info_compra = ref("")
let acciones= ref(false)

const balotas = ref([]);
const balotas_compradas = ref([]);

const crearBalotas = () => {
  const [start, end] = seleccion_numboletas.value.split("-").map(Number);
  card1.value = true;
  for (let i = start; i <= end; i++) {
    balotas.value.push({
      item: i,
    });
  }

  bd.value = false;
};
let balota_elegida = ref(null);

const registrar_balota = (i) => {
  balota_elegida.value = i;
  registro_balota.value = true;
};

const agregar = () => {
  registro_balota.value = false;
  balotas_compradas.value.push({
    numero: balotas.value[balota_elegida.value].item,
    nombre: nombre_persona.value,
    telefono: telefono.value,
    direccion: direccion.value,
    pagos: seleccion_pago.value,
  });
};
console.log(balotas_compradas);
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  background-color: white;
}

.contenedor {
  width: 100%;
  height: 100vh;
}

.titulo {
  height: 100px;
  display: flex;

  width: 100%;
  align-items: center;
  justify-content: center;
  background-color: rgb(38, 38, 151);
}

.text_tit {
  font-size: 40px;
  color: white;
}

.text_pie {
  font-size: 20px;
  color: white;
}
.footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 40px;
  background-color: rgb(38, 38, 151);
  text-align: center;
  padding-top: 5px;
}

.modal-body {
  display: grid;
  gap: 1px;
}

.cuerpo {
  width: 100%;
  height: auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

.cont_2 {
  width: 50%;
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  margin-top: 50px;
}
.balotas {
  display: flex;
  flex-wrap: wrap;
}

.balota {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: blue;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 5px;
  cursor: pointer;
}

.balota:hover {
  transform: scale(1.1);
}

.cont1 {
  width: 100%;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

.card1 {
  width: 70%;
  height: auto;
  display: grid;
  grid-template-rows: repeat(6, 1fr);
  background-color: blue;
}

.info {
  font-size: 30px;
  color: rgb(0, 0, 0);
}
</style>
