
<template>
  <div>
    <el-form :model="ruleForm"
             :rules="rules"
             ref="ruleForm"
             label-width="100px"
             class="demo-ruleForm"
             size="mini">
      <el-table :data="ruleForm.tableData"
                style="width: 100%">
        <el-table-column label="姓名"
                         width="180">
          <template slot-scope="scope">
            <el-form-item :prop="'tableData.' + scope.$index + '.name'"
                          :rules="rules.name">
              <el-input v-model="scope.row.name"
                        autocomplete="off"></el-input>
            </el-form-item>
          </template>
        </el-table-column>
        <el-table-column label="地址">
          <template slot-scope="scope">
            <el-form-item :prop="'tableData.' + scope.$index + '.address'"
                          :rules="rules.address">
              <el-input v-model="scope.row.address"
                        autocomplete="off"></el-input>
            </el-form-item>
          </template>
        </el-table-column>
      </el-table>
    </el-form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      ruleForm: {
        tableData: [{
          name: '',
          address: ''
        }, {
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          name: '',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          name: '王小虎',
          address: ''
        }]
      },
      rules: {
        name: [
          {
            validator: (rule, value, callback) => {
              const row = +rule.field.split('.')[1]
              console.log(`name validator row:${row} name:${value} address:${this.ruleForm.tableData[row].address}`)
              if (value === '') {
                callback(new Error('请输入姓名'))
                return
              }
              callback()
            }
          }
        ],
        address: [
          {
            validator: (rule, value, callback) => {
              const row = +rule.field.split('.')[1]
              console.log(`address validator row:${row} name:${value} address:${this.ruleForm.tableData[row].address}`)
              if (value === '') {
                callback(new Error('请输入地址'))
                return
              }
              callback()
            }
          }
        ]
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