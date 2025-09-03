<template>
  <div>
    <p>{{ nome }}</p>
    <p>
      <label id="labelusuario" for="usuario">Nome: </label>
      <input id="usuario" v-model="nome" />
      <input id="usuario2" :value="nome" />
    </p>
    <p>
      <label id="labelsenha" for="senha">Senha: </label>
      <input id="senha" type="password" v-model="senha" />
    </p>
    <p v-if="senha.length < 5">Senha muito curta!</p>
    <p v-else>Senha ok!</p>
    <button @click="inserirUsuario">Cadastrar</button>
    <table>
      <thead>
        <tr>
          <th>Id</th>
          <th>Nome</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="usuario in usuarios" :key="usuario.id">
          <th>{{ usuario.id }}</th>
          <th>{{ usuario.nome }}</th>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface usuario {
  id?: number
  nome: string
  senha: string
}

const nome = ref<string>('Teste')
const senha = ref<string>('123')
const cont = ref<number>(3)

const usuarios = ref<usuario[]>([
  {
    id: 1,
    nome: 'admin',
    senha: 'admin',
  },
  {
    id: 2,
    nome: 'teste',
    senha: '123',
  },
])

function inserirUsuario() {
  usuarios.value.push({ id: cont.value++, nome: nome.value, senha: senha.value })
  nome.value = ''
  senha.value = ''
}
</script>
