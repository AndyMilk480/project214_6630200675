<template>
  <div class="stuForm">
    <div class="stuForm2">
      <!--แบบฟอร์มแก้ไขข้อมูลนิสิต-->
      <div class="formHeader">
        <h3>แก้ไขข้อมูลนิสิต</h3>
      </div>
      <form class="formDetail" id="studentForm" @submit.prevent="formsubmit">

          <label for="name">ชื่อ</label><br>
          <input type="text" id="name" v-model ="formData.studentname" required><br>

          <label for="id">รหัสนิสิต</label><br>
          <input type="text " id="id" v-model ="formData.studentID" required><br>

          <label for="major">สาขา</label><br>
          <input type="text" id="major" v-model ="formData.major" required><br>

          <label for="school">โรงเรียน</label><br>
          <input type="text" id="school" v-model ="formData.school" required><br>

          <button class="save" type="submit">บันทึก</button>
      </form>
  </div>
    </div>
</template>

<script>
import { Eventbus } from '@/event-bus'
export default {
    name:"StudentForm",
    data(){
      return{
        formData:{}
      }
    },
    methods:{
      formsubmit(){

        fetch("http://localhost:3000/Student",{
          method:"PUT",
          headers: {"content-type": "application.json"},
          body: JSON.stringify(this.formData)
        })
        .then(() => {
          Eventbus.emit("studentchange", {message:'edit'})
        })
      }
    }
}
</script>

<style scoped>
  .stuForm{
    background-color: #ffffff;
  }
  .stuForm2{
    margin: 15px;
  }
  *{
    color: rgb(132, 132, 132);
  }
  .save{
    margin-top: 10px;
    border: none;
    border-radius: 4px;
    background-color:#ff9800;
    padding: 4px 15px;
    color: rgb(255, 255, 255);
    transition: 0.3s;
  }
  input{
    border-radius: 4px;
    border: 1px solid rgb(192, 192, 192);
  }
  input:hover{
    border: 1px solid rgb(116, 197, 255);
  }
  input:focus{
      border: 2px solid rgb(116, 197, 255);
  }
  .save:hover {
    background-color: #e68900;
  }
  @media (max-width: 1258px){
    .stuForm{
      margin: 50px;
      width: 230px;
    }
  }
</style>