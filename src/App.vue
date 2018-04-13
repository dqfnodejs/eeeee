<template>
  <div class="hello">

    <p>课程表</p>
    <el-table
    :data="arr"
    stripe
    style="width: 100%">
    <el-table-column
      prop="jie"
      label="课程/时间">
    </el-table-column>
    <el-table-column
      prop="Monday"
      label="星期一">
    </el-table-column>
    <el-table-column
      prop="Tuesday"
      label="星期二">
    </el-table-column>
    <el-table-column
      prop="Wednesday"
      label="星期三">
    </el-table-column>
    <el-table-column
      prop="Thursday"
      label="星期四">
    </el-table-column>
    <el-table-column
      prop="Friday"
      label="星期五">
    </el-table-column>
  </el-table>
    
    
    <el-button type="text" @click="dialogFormVisible = true">更改课程</el-button>

    <el-dialog title="课程更改" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="星期一" :label-width="formLabelWidth">
          <el-input v-model="form.Monday" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="星期二" :label-width="formLabelWidth">
          <el-input v-model="form.Tuesday" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="星期三" :label-width="formLabelWidth">
          <el-input v-model="form.Wednesday" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="星期四" :label-width="formLabelWidth">
          <el-input v-model="form.Thursday" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="星期五" :label-width="formLabelWidth">
          <el-input v-model="form.Friday" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="第几节" :label-width="formLabelWidth">
          <el-select v-model="form.o" placeholder="请选择第几节">
            <el-option label="一" value="1"></el-option>
            <el-option label="二" value="2"></el-option>
            <el-option label="三" value="3"></el-option>
            <el-option label="四" value="4"></el-option>
            <el-option label="五" value="5"></el-option>
            <el-option label="六" value="6"></el-option>
            <el-option label="七" value="7"></el-option>
            <el-option label="八" value="8"></el-option>
          </el-select>
        </el-form-item>
      </el-form>  
      <div slot="footer" class="dialog-footer">
        <el-button type="primary" @click="submit">确 认</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      arr:[],
       dialogFormVisible: false,
        form: {
          Monday:'数学',
          Tuesday:'数学',
          Wednesday:'数学',
          Thursday:'数学',
          Friday:'数学',
          o:''
        },
        formLabelWidth: '120px'
    }
  },
  created(){
    this.qi()
  },
  methods:{
    qi(){
      this.$http.get('http://localhost:3000/',{},{emulateJSON:true}).then(e=>this.arr=e.body)
    },
    submit(){
      this.dialogFormVisible=false,
      this.$http.post('http://localhost:3000/updata',this.form,{emulateJSON:true}).then(()=>{
        this.qi()
      })
    }
  }
}
</script>
<style>
    p{
        text-align: center;
    }
</style>