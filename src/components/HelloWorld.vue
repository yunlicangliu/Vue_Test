<template>
  <div class="hello">
    <h1 @click="messageSend">{{ msg }}</h1>
    <el-form ref="form" :model="form" label-width="80px" class="myForm">
      <el-form-item label="姓名">
        <el-input v-model="form.name"></el-input>
      </el-form-item>
      <el-form-item label="问候">
        <el-input placeholder="请输入你的问候" v-model="form.hello"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">提交</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Please click me then see console',
      form: {
        name: '',
        hello: ''
      }
    }
  },
  methods: {
    onSubmit () {
      let that = this
      this.$axios.post('/post', {
        name: that.form.name,
        hello: that.form.hello
      }).then(res => {
        console.log(res.data)
      }).catch(e => {
        console.log(e)
      })
    },
    messageSend () {
      this.$axios.get('/hello')
        .then(res => {
          console.log(res.data)
        }).catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
a {
  color: #42b983;
}
.myForm {
  width: 30%;
  margin: auto;
}
</style>
