<template>
    <div>
      <h2>Cadastro de Itens</h2>
      <form @submit.prevent="addItem">
        <input 
          type="text" 
          v-model="newItem.name" 
          placeholder="Nome do item" 
          required 
        />
        <input 
          type="number" 
          v-model="newItem.quantity" 
          placeholder="Quantidade" 
          min="1" 
          required 
        />
        <button type="submit">Cadastrar</button>
      </form>
      
      <div v-if="items.length > 0">
        <h3>Lista de Itens</h3>
        <ul>
          <li v-for="(item, index) in items" :key="index">
            {{ item.name }} - Quantidade: {{ item.quantity }}
          </li>
        </ul>
      </div>
      <div v-else>
        <p>Nenhum item cadastrado.</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newItem: {
          name: '',
          quantity: 1,
        },
        items: [],
      };
    },
    methods: {
      addItem() {
        this.items.push({ ...this.newItem });
        this.newItem.name = '';
        this.newItem.quantity = 1;
      },
    },
  };
  </script>
  
  <style scoped>
  form {
    margin-bottom: 20px;
  }
  input {
    margin-right: 10px;
  }
  button {
    padding: 5px 10px;
  }
  ul {
    list-style: none;
    padding: 0;
  }
  li {
    margin: 5px 0;
  }
  </style>
  