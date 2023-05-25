<template class="color">
  <body>
    <section>
      <h1 class="titulo">
        Bienvenidos al formulario de VUE
      </h1>
      <section id="app" class="orden color">

        <form @submit.prevent="submitForm">
          <article class="txt">
            <label for="name">Nombre:</label>
            <input type="text" id="name" v-model="name" required>
          </article>
          <br>
          <article class="txt">
            <label for="ape">Apellido:</label>
            <input type="text" id="ape" v-model="ape" required>
          </article>
          <br>
          <article class="txt">
            <label for="age">Edad: </label>
            <input type="number" id="age" v-model="age" required min="1">
          </article>
          <br>
          <article class="txt">
            <label for="cc">Cedula: </label>
            <input type="number" id="cc" v-model="cc" required>
          </article>
          <br>
          <button class="btn_g" type="submit">Enviar</button>
        </form>
          <ul>
            <li class="txt" v-for="(persona, index) in personas" :key="index">
              {{persona.name}} {{persona.ape}} - Edad: {{persona.age}} - Cedula: {{persona.cc}}
              <button class="btn_e" @click="borrar(index)"> Borrar usuario</button>
            </li>
          </ul>

      </section>
      

      <p>Ahora somos {{ mayor_ed }} menores de edad</p>
      <p>Ahora somos {{ menor_ed }} menores de edad</p>
    </section>
  </body>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      ape: "",
      age: null,
      cc: null,
      mayor_ed: 0,
      menor_ed: 0,
      personas: []
    };
  },
  methods: {
    submitForm() {
      this.personas.push({
        name: this.name,
        ape: this.ape,
        age: this.age,
        cc: this.cc
      });
      this.name = '';
      this.ape = '';
      this.age = null;
      this.cc = null;
    },
    agregar(event) {
      event.preventDefault();
      const nueva ={
        name: this.name,
        ape: this.ape,
        age: this.age,
        cc: this.cc
      };

      this.personas.push(nueva);
      
      if (nueva.age >=18){
        this.mayor_ed++
      } else {
        this.menor_ed++
      }

      this.resetForm();
    },
    borrar(index){
      const borrar = this.personas[index];
      if (borrar.age >=18){
        this.mayor_ed--
      } else {
        this.menor_ed--
      }

      this.personas.splice(index, 1)
    },
    resetForm(){
      this.name = "",
      this.ape = "",
      this.age = null, 
      this.cc = null
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.titulo {
  text-align: center;
}
.orden {
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.txt {
  color: #35495E;
  margin-top: 20px;
  font-family: 'Courier New', Courier, monospace;
  font-size: larger;
  font-weight: bold;
}

.color {
    background-color: #41B883;
    padding: 20px;
}

.btn_g {
    background-color: #4CAF50;
    color: white;
    padding: 10px 20px;
    border: none;
    cursor: pointer;
}

.btn_e {
    background-color: #f44336;
    color: white;
    padding: 5px 10px;
    border: none;
    cursor: pointer;
}
</style>
