<template>
  <div id="app">
    <el-row>
      <el-col :span="20" :pull=2 :push=2>
        <log v-for='i in list' :info='i'></log>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import Log from './components/Log.vue'
export default {
  name: 'app',
  data () {
    return {
      list: []
    }
  },
  components: {
    Log
  },
  created (){
    var self = this
    var config = {
      syncURL: "https://niwa.wilddogio.com"
    }
    wilddog.initializeApp(config)
    var ref = wilddog.sync().ref('/rest/daocloud/webhook')
    ref.limitToLast(15).on('child_added', data => {
      self.list.unshift(data.val())
    })
  }
}
</script>

<style>
.el-alert {
  margin: 20px 0 0;
}
</style>
