<template>
  <div>
    <div>
      <label for="nome_aluno">Nome aluno: </label>
      <input type="text" id="nome" v-model="nome">
    </div>
    <br><br>
    <div>
      <label for="nota1">Nota1:  </label>
      <input type="number" id="nota1" v-model="nota1">
  
      <label for="nota2">Nota2:  </label>
      <input type="number" id="nota2" v-model="nota2">
  
      <label for="nota3">Nota3:  </label>
      <input type="number" id="nota3" v-model="nota3">
    </div><br>
    <button @click="inserir()">Inserir</button> 

    <div>
      <table>
        <tr>
          <td></td>
          <td></td>
        </tr>
        <tr>
          <th>Nome</th>
          <th>Média</th>
          <th>Situação</th>
        </tr>
        <tr v-for="a in alunos" :key="a.nome"> 
          <td>{{ a.nome }}</td>
          <td>{{ a.media }}</td>
          <td :class="{ 'cor': cor_texto }">{{ a.situacao }} </td>
        </tr>
      </table>
    </div>
  </div>
  
</template>

<script>

export default {
  data() {
    return {
      alunos: [{
          nome: '',
          nota1: null,
          nota2: null,
          nota3: null,
          media: null,
          situacao: null
    }],
      texto: '',
    }
  }, 
  methods: {
    
    calculaMedia() {
      this.media = (this.nota1 + this.nota2 * 2 + this.nota3 * 3)/7
      parseInt(this.media)
      return this.media
    },
    
    getSituacao() {
      if (this.media >= 7) {
        this.situacao = 'Aprovado'
        this.cor_texto = true
      } else {
        this.situacao = 'Reprovado'
        this.cor_texto = false
      }
      return this.situacao
      
    },
    inserir() {
      this.alunos.push({
          nome: this.nome,
          nota1: this.nota1,
          nota2:this.nota2,
          nota3: this.nota3,
          media: this.calculaMedia(),
          situacao: this.getSituacao()
      });
      
      console.log(this.alunos)
    },
  }


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.cor {
  color: blue
}
</style>
