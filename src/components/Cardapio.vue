<template lang="html">
  <div class="teste">
    <div class="card" v-for="card in cards">
      <h1> {{card.titulo}}</h1>
      <h6>Codigo: {{card.cod}}</h6>
      <h3>Ingredientes:</h3>
      <ul>
        <li class="chip" v-for="ingredientes in card.ingredientes">{{ingredientes}}</li>
      </ul>
      <h5>Descrição:</h5>
      <p>{{card.descricao}}</p>
      <h5>Valor: {{card.valor}}</h5>
      <div class="footer_card">

        <div class="botao_bola" @click="deletar(card.cod)" id="botao_bola1" >
          <span class="material-icons">delete</span>
        </div>
        <div class="botao_bola" @click="navegar_ficha_tecnica(card.cod)" id="botao_bola2" >
        <span class="material-icons">create</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import db from '@/firebase/init'
  export default {
    name:'Cardapio',
    data(){

      return{
        cards:[]
  }
    },
    created(){
      db.collection('cardapio').get()
      .then(snapshot => {
        snapshot.forEach(doc => {

          let prato = doc.data()
          // prato.cod = mentira que irado doc.cod teste teletype 2
            console.log(prato.cod)
          this.cards.push(prato)
        })
      })
    },
    methods:{
    navegar_ficha_tecnica(cod){
        this.$router.push({ name: 'Cadastro_ficha_tecnica', params:{cod:cod}})
    },
    deletar(cod){
      alert(cod)
      db.collection('cardapio').doc(cod).delete();

    }
    }
}
</script>

<style scoped>

.footer_card{
  position:inherit;
  width: 100%;
}
.card{
  display: inline-block;
  margin-top: 5%;
  margin-left: 50px;
  width: 350px;
  height: 400;
  border: 0px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  text-align: center;

}
#botao_bola1{
  margin-bottom: -50px;
  margin-left: 5%;
  margin-right:auto;
}
#botao_bola2{
  margin-bottom: -25px;
  margin-left: auto;
  margin-right:5%;
}
.chip {

  display: inline-block;
  padding: 0 5px;
  margin: 2%;
  margin-right: auto;
  height: 35px;
  font-size: 14px;
  line-height: 35px;
  border-radius: 20px;
  background-color: #C5CAE9;
}
</style>
