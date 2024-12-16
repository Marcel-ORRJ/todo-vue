<script setup>
import { reactive } from 'vue';

const nome = "Marcelo"
const meuObj = {
  nome: "Marcelo",
  fileFavorito: "Rocky"
}

function dizOla(nome) {
  return `${nome} diz oi`
}

const enderecoImagemBatman = "https://ingresso-a.akamaihd.net/b2b/production/uploads/article/image/1625/michael-keaton-o-ator-que-moldou-o-jeito-de-ser-o-batman-nos-cinemas-39c197523c5cc4.jpg"
const enderecoImagemSuperman = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSeRaxgqEVBX4jF4Ul3jzOJFElZY8eI6A57QA&s"

const botaHabilitado = false

const gostaDoBatman = false
const gostaDoSuperman = false

const estaAutorizado = false

// let contador = 0
const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['gian', 'paulo', 'luisa', 'monica', 'pedro'],
  nomeAInserir: '',
})

function incrementar() {
  estado.contador++
}

function decrementar() {
  estado.contador--
}

function alteraEmail(evento) {
  estado.email = evento.target.value
}

function mostraSaldoFuturo() {
  const { saldo, transferindo } = estado
  return saldo - transferindo
}

function validaValorTransferencia() {
  const { saldo, transferindo } = estado
  return saldo >= transferindo
}

function cadastraNome() {
  if (estado.nomeAInserir.length < 3) {
    alert("Nome inválido")
  } else {
    estado.nomes.push(estado.nomeAInserir)
  }
}
</script>

<template>
  <h1>{{ dizOla("Paula") }}</h1>
  <img v-if="gostaDoBatman" :src="enderecoImagemBatman" alt="">
  <img v-else-if="gostaDoSuperman" :src="enderecoImagemSuperman" alt="">
  <h2 v-else>Não Curte heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem-vindo</h1>
  <h1 v-else="estaAutorizado">Não possui acesso</h1>

  <button :disabled="!botaHabilitado">Enviar Mensagem</button>
  <br/>
  <hr/>
  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar"  type="button">-</button>

  <br/>
  <hr/>

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail">

  <br/>
  <hr/>

  Saldo: {{ estado.saldo }}
  <br/>
  Transferindo: {{ estado.transferindo }}
  <br/>
  Saldo após a transferência: {{ mostraSaldoFuturo() }}
  <br/>
  <input class="campo" :class="{ invalido: !validaValorTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia a transferir"/>
  <button v-if="validaValorTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br/>
  <hr/>

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button @click="cadastraNome()" type="button">Cadastrar novo nome</button>

  <h3 v-for="nome in estado.nomes">{{ nome }}</h3>
</template>

<style scoped>
img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
  border-color: red;
}

.campo {
  border: 2px solid #000
}
</style>