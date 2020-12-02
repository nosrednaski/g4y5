<template>
  <div>
    <input type="search" v-model='query'>
    <button type="submit" @click='submit'>Submit</button>
  </div>

  <section>
    <template v-for="(toDo, i) in toDos" :key='i'>
      <button @click='done(toDo)' :class="{ 'crossed-out' : toDo.bool }" >
        {{ toDo.title }}
      </button>
      
    </template>
  </section>
</template>

<script>
export default {
  data() {
    return {
      query: null,
      toDos: [],
    }
  },
  methods: {
    submit() {
      this.toDos.push({
        title: this.query,
        bool: false
      })
    },
    done(toDo) {
      toDo.bool = !toDo.bool
    }
  },
  async created() {
    const res = await fetch("https://todo-cf583.firebaseio.com/")
    console.log(res)
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
input {
  margin-bottom: 4vh;
  margin-right: 1vw;
}
section > button {
  display: block;
  margin: .5rem auto;
}
.crossed-out {
  text-decoration: line-through;
}
</style>
