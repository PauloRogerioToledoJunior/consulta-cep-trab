<template>
  <div>
    <h1 style="text-align: center;">Consultar CEP</h1>
    <div class="container">
      <div class="left">
        <form action="#" onsubmit="event.preventDefault()">
          <label for="cep">Digite o CEP</label>
          <br>
          <input type="text" id="cep" v-model="cep" />
          <br />
          <br>
          <label for="formato">Selecione o formato </label>
          <br>
          <select v-model="selectedFormat">
            <option value="/json">json</option>
            <option value="/xml">xml</option>
          </select>
          <br />
          <input class="btn" type="submit" value="Consultar" @click="getCep" />
        </form>
      </div>
      <div class="center">
        <span id="status"></span>
        <p style="font-size: 60px; text-align: center;">👉</p>
        
      </div>
      <div class="rigth">
        <div>
          <p>Rua: {{ place.street }}</p>
          <p>Bairro: {{ place.neighborhood }}</p>
          <p>Cidade: {{ place.city }} - {{ place.state }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { reactive, ref } from "vue";

const baseUrl = "https://viacep.com.br/ws/";

const cep = ref("");
const selectedFormat = ref("/json");

const place = reactive({
  street: "",
  neighborhood: "",
  city: "",
  state: "",
});

const getCep = () => {
  console.log(selectedFormat);
  axios
    .get(baseUrl + cep.value + selectedFormat.value)
    .then((response) => {
      console.log(response);
      (place.street = response.data.logradouro),
        (place.neighborhood = response.data.bairro),
        (place.city = response.data.localidade),
        (place.state = response.data.uf);
        document.getElementById("status").innerHTML = `
        <p style="background: rgb(108, 189, 108);color: white;font-weight: bold;padding: 8px 16px; border-radius: 8px;">Deu bom! 😊</p> 
        ` 
    })
    .catch((error) => {
      console.error("Eita.. deu erro!", error);
      document.getElementById("status").innerHTML = `
        <p style="background: rgb(220, 79, 66);color: white;font-weight: bold;padding: 8px 16px; border-radius: 8px;">Deu ruim! 😥</p> 
        `  
    });
};
</script>

<style scoped>
.btn {
  border: 0;
  color: white;
  cursor: pointer;
  font-weight: bold;
  background: linear-gradient(to left, rgb(153, 0, 255), rgb(21, 0, 255));
  border-radius: 6px;
  padding: 8px 16px;
  margin-top: 25px;
}
.btn:hover {
  background: linear-gradient(to left, rgb(190, 93, 254), rgb(90, 75, 255));
}
.container{
    display: flex;
    width: 100vw;
    justify-content: space-evenly;
    align-items: center;
}

.left{
    padding: 20px 30px;
    background: #ccc;
    border-radius: 8px;
}

.center{
    align-items: flex-start;
}

.rigth{
    padding: 20px 20px;
    width: 230px;
    max-width: 250px;
    background: #ccc;
    border-radius: 8px;
}

input{
    border: 0;
    border-radius: 6px;
    height: 26px;
    padding-left: 8px;
}

select{
    border: 0;
    border-radius: 6px;
    height: 26px;
}
</style>