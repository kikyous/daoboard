<template>
  <el-alert
    :title="title"
    :type="type"
    :description="description"
    :closable='false'
    show-icon>
  </el-alert>
</template>
<script>
export default {
  props: ['info'],
  computed: {
    title (){
      return `${this.info.build.author} : ${this.info.build.message}`
    },
    type (){
      return {'Pending': 'info', 'Started': 'warning', 'Failure': 'error', 'Success': 'success', 'Error': 'error'}[this.info.build.status];
    },
    time (){
      switch (this.info.build.status) {
        case 'Success':
          return `耗时${this.info.build.duration_seconds}s`
        case 'Pending':
          return ''
        default: {
          var d = new Date(this.info.build.started_at)
          return d.toLocaleString()
        }
      }
    },
    description (){
      return `${this.status_text} • ${this.time}`
    },
    status_text (){
      return {'Pending': '准备构建', 'Started': '开始构建', 'Error': '发生错误', 'Failure': '构建失败', 'Success': '构建成功'}[this.info.build.status]
    }
  },
}
</script>
