<template>
  <div>
    <h1>{{ msg }}</h1>
    <form @submit.prevent="getCat">
      <div class="form__input-container">
       
        <div class="row form-group">
          <div class="col-6 d-flex flex-column align-items-end">
            <label for="text">Título</label>
            <label for="text">Filtro</label>
            <label for="text">Color</label>
            <label for="text">Tamaño</label>
          </div>
          
          <div class="col-6 d-flex flex-column align-items-start">
            <input type="text" v-model="title">
            <select v-model="filter">
              <option disabled value="">Seleciona un filtro</option>
              <option>Blur</option>
              <option>Mono</option>
              <option>Sepia</option>
              <option>Negative</option>
              <option>Paint</option>
              <option>Pixel</option>
            </select>
            <div class="d-flex">
              <select v-model="color">
                <option disabled value="">Seleciona un Color</option>
                <option value="red">Rojo</option>
                <option value="blue">Azul</option>
                <option value="green">Verde</option>
                <option value="white">blanco</option>
                <option value="yellow">amarillo</option>     
              </select>
              <span class="circle" :style="{'background-color':color}"></span>
            </div>
            <input type="number" v-model.number="size">
          </div>
        </div>
      </div>
      <input class="mt-3" type="submit" value="Obtener mi gatito">
    </form>
    
    <div class="spinner-border" :class="{'d-none': !loading}" role="status" >
      <span :class="sr-only">Cat</span>
    </div>
    <img :src="image">

  </div>
</template>

<script>
export default {
  name: 'RandomCat',
  props: {
    msg: String,
  },
  data() {
    return {
      filter: "",
      color: "",
      size: 100,
      image: "",
      title: "",
      loading: false,
    }

  },
  methods: {
    getCat() {
      this.loading = true;
      fetch(`https://cataas.com/cat/gif/says/${this.title}?filter=${this.filter}&color=${this.color}&size=${this.size}`)
      .then((data) => {
        this.image = data.url;
        this.loading = false;
      });
  },
},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
h1 {
  font-size: 2em;
  font-weight: 700;
  text-align: center;
  padding: 2em 0 1em;
}
.form__input-container {
  background-color: lightcoral;
  padding: 2em;
}
.circle {
  height: 20px;
  width: 20px;
  border-radius: 50% ;
  display: inline-block;
  margin-left: 1em;
}

</style>