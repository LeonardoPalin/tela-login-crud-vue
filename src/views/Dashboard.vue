<template>
  <div class="dashboard-wrapper">
    <div class="dashboard-card">
      <div class="header">
        <h1>📚 Painel Acadêmico</h1>
        <button class="logout" @click="logout">Sair</button>
      </div>

      <div class="crud-area">
        <h2>👥 Gerenciar Estudantes</h2>

        <div class="form">
          <input v-model="novoNome" placeholder="Nome do estudante" />
          <input v-model="novoEmail" placeholder="Email do estudante" />
          <button class="add-btn" @click="adicionarEstudante">Adicionar</button>
        </div>

        <ul class="lista">
          <li v-for="(estudante, index) in estudantes" :key="index">
            <span>{{ estudante.nome }} - {{ estudante.email }}</span>
            <button class="remover-btn" @click="removerEstudante(index)">Remover</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { getAuth, signOut } from "firebase/auth";

export default {
  data() {
    return {
      novoNome: "",
      novoEmail: "",
      estudantes: JSON.parse(localStorage.getItem("estudantes")) || []
    };
  },
  methods: {
    logout() {
      const auth = getAuth();
      signOut(auth).then(() => {
        this.$router.push("/");
      });
    },
    adicionarEstudante() {
      if (this.novoNome && this.novoEmail) {
        this.estudantes.push({ nome: this.novoNome, email: this.novoEmail });
        this.salvar();
        this.novoNome = "";
        this.novoEmail = "";
      }
    },
    removerEstudante(index) {
      this.estudantes.splice(index, 1);
      this.salvar();
    },
    salvar() {
      localStorage.setItem("estudantes", JSON.stringify(this.estudantes));
    }
  }
};
</script>

<style scoped>
.dashboard-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 4rem 1rem;
  background: linear-gradient(to right, #f0f4ff, #e6ecfa);
  min-height: 100vh;
}

.dashboard-card {
  background: white;
  border-radius: 16px;
  padding: 2rem 2rem;
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.08);
  max-width: 800px;
  width: 100%;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

h1 {
  font-size: 1.8rem;
  color: #1a237e;
}

.logout {
  background: #ff5252;
  border: none;
  color: white;
  padding: 0.5rem 1.2rem;
  font-weight: bold;
  border-radius: 10px;
  cursor: pointer;
  transition: background 0.3s;
}

.logout:hover {
  background: #e53935;
}

h2 {
  font-size: 1.4rem;
  margin-bottom: 1rem;
  color: #333;
}

.form {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

input {
  flex: 1;
  min-width: 180px;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.add-btn {
  background: #4caf50;
  border: none;
  color: white;
  padding: 0.5rem 1.2rem;
  font-weight: bold;
  border-radius: 10px;
  cursor: pointer;
  transition: background 0.3s;
}

.add-btn:hover {
  background: #388e3c;
}

.lista {
  list-style: none;
  padding: 0;
}

.lista li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f5f5f5;
  margin-bottom: 0.5rem;
  padding: 0.6rem 1rem;
  border-radius: 8px;
}

.remover-btn {
  background: #d32f2f;
  border: none;
  color: white;
  padding: 0.3rem 0.8rem;
  font-size: 0.9rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s;
}

.remover-btn:hover {
  background: #b71c1c;
}
</style>
