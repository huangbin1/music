<template>
  <div class="MessageLength">
    <ul>
      <input v-model="message" placeholder="edit me">
      <p>Message is: {{ message }}</p>
      <p>Message Length is: {{ LengthMessage }}</p>
      
    </ul>
      <button @click="xiaojiji">增加 1</button>
      <p>'夏晓雯蛋蛋有 '{{ counter }} 个。</p>
  </div>
</template>

<script>
export default {
  name: 'MessageLength',
  data () {
    return {
      message:'xiaoxiawenjijixiao',
      LengthMessage:0,
      counter:0

    }
  },
  watch: {
    message: function (val, oldVal) {
      console.log('new: %s, old: %s', val.length, oldVal.length)
      this.LengthMessage=val.length
    }
  },
  methods: {
    xiaojiji: function (event) {
      // `this` 在方法里指当前 Vue 实例
      this.counter++;
      
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
