<template>
  <div>
    <h2>Gerenciar Estudantes</h2>
    <input v-model="novoNome" placeholder="Nome do estudante" />
    <input v-model="novoEmail" placeholder="Email do estudante" />
    <button @click="adicionarEstudante">Adicionar</button>

    <ul>
      <li v-for="(estudante, index) in estudantes" :key="index">
        {{ estudante.nome }} - {{ estudante.email }}
        <button @click="removerEstudante(index)">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      novoNome: '',
      novoEmail: '',
      estudantes: JSON.parse(localStorage.getItem('estudantes')) || []
    }
  },
  methods: {
    adicionarEstudante() {
      if (this.novoNome && this.novoEmail) {
        this.estudantes.push({ nome: this.novoNome, email: this.novoEmail });
        this.salvar();
        this.novoNome = '';
        this.novoEmail = '';
      }
    },
    removerEstudante(index) {
      this.estudantes.splice(index, 1);
      this.salvar();
    },
    salvar() {
      localStorage.setItem('estudantes', JSON.stringify(this.estudantes));
    }
  }
}
</script>
