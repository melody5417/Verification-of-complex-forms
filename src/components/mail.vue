
<template>
  <div>
    <el-form :model="ruleForm"
             :rules="rules"
             ref="ruleForm"
             label-width="100px"
             class="demo-ruleForm"
             size="mini">
      <el-form-item label="主题"
                    prop="title">
        <el-input v-model="ruleForm.title"></el-input>
      </el-form-item>
      <el-form-item label="内容"
                    prop="content">
        <el-input v-model="ruleForm.content"></el-input>
      </el-form-item>
    </el-form>
  </div>

</template>

<script>
export default {
  data () {
    return {
      ruleForm: {
        content: '',
        title: ''
      },
      rules: {
        content: [
          { required: true, message: "请输入内容", trigger: "blur" },
        ],
        title: [
          { required: true, message: "请输入主题", trigger: "blur" },
        ],
      }
    };
  },
  methods: {
    validate () {
      return new Promise((resolve, reject) => {
        this.$refs.ruleForm.validate((valid, field) => {
          console.log(valid, field)
          if (valid) {
            resolve(true)
          } else {
            reject(new Error(Object.values(field)[0][0].message))
          }
        })
      })
    },
    getData () {
      return this.ruleForm
    },
    resetForm () {
      this.$refs['ruleForm'].resetFields();
    },
  }
};
</script>