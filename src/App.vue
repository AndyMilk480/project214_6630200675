<template >
  
  <div >
    <div class="stuPack">
      <!-- แสดงชื่อนิสิต และฟอร์สำหรับแก้ไข -->
      <student></student>
      <student-form></student-form>
    </div>

    <!--แสดง/เพื่ม/ลบ/แก้ไข วิชา-->
    <subject></subject>
  </div>

  <!-- ชื่อ นามสกุล -->
  <div class="endCredit">
    <p>พัตนาโดย นายอันเดรียส เนตเซล 6630200675</p>
    <p>Project 214 | Practicum in Software Development</p>
  </div>

</template>

<script>

import StudentForm from './components/StudentForm.vue'
import Student from './components/Student.vue'
import Subject from './components/SubjectList.vue'

export default {
  name: "App",
  components: {
    Student,
    StudentForm,
    Subject
  },
}
</script>

<style scoped>
  .stuPack{
    display: flex;
    justify-content: center;
    margin: 50px;
  }
  .endCredit{
    background-color: #222;
    text-align: center;
    padding: 4px 15px;
  }
  @media (max-width: 1258px){
    .stuPack{
      display: flex;
      flex-direction: column;
      justify-content: center;
      margin: auto
    }
  }
</style>
