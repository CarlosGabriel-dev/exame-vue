<template>
  <div class="container">
    <div class="card">
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
        <button type="submit">{{ isEditing ? "Salvar Alterações" : "Cadastrar" }}</button>
      </form>
      
      <div v-if="items.length > 0">
        <h3>Lista de Itens</h3>
        <ul>
          <li v-for="(item, index) in items" :key="index">
            {{ item.name }} - Quantidade: {{ item.quantity }}
            <button class="edit-btn" @click="editItem(index)">Editar</button>
            <button class="delete-btn" @click="deleteItem(index)">Excluir</button>
          </li>
        </ul>
      </div>
      <div v-else>
        <p>Nenhum item cadastrado.</p>
      </div>
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
      isEditing: false,
      editIndex: null,
    };
  },
  methods: {
    addItem() {
      if (this.isEditing) {
        this.items[this.editIndex] = { ...this.newItem };
        this.isEditing = false;
        this.editIndex = null;
      } else {
        this.items.push({ ...this.newItem });
      }
      this.resetForm();
    },
    editItem(index) {
      this.newItem = { ...this.items[index] };
      this.isEditing = true;
      this.editIndex = index;
    },
    deleteItem(index) {
      this.items.splice(index, 1);
    },
    resetForm() {
      this.newItem = { name: '', quantity: 1 };
    },
  },
};
</script>

<style scoped>

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f3f4f6; 
}

.card {
  background-color: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  width: 400px;
  text-align: center;
  color: black; 
}

form {
  margin-bottom: 20px;
}
input {
  width: calc(50% - 10px);
  padding: 8px;
  margin: 5px 0;
  border: 1px solid #ccc;
  border-radius: 4px;
}
button {
  padding: 8px 12px;
  margin: 5px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button[type="submit"] {
  background-color: #4caf50;
  color: white;
}
button.edit-btn {
  background-color: #2196f3;
  color: white;
}
button.delete-btn {
  background-color: #f44336;
  color: white;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ddd;
  color: black; 
}
</style>
