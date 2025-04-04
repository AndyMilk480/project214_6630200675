<template>
    <div class="form">
        <!--แบบฟอร์เพื่มวิชา-->
        <form id="subjectForm" @submit.prevent="subjectsubmit">

            <label for="subid">รหัสวิชา</label>
            <input type="text" id="subid" v-model ="subjectForm.subjectID" required>

            <label for="subname">ชื่อวิชา</label>
            <input type="text" id="subname" v-model ="subjectForm.subjectname" required><br>

            <label for="credit">หน่วยกิต</label>
            <input type="number" id="credit" v-model ="subjectForm.credit" required>

            <label for="grade">เกรด</label>
            <input type="text" id="grade" v-model ="subjectForm.grade" required><br>

            <button class="addBut" type="submit">Submit</button>

        </form>
    </div>
</template>

<script>
import {Eventbus} from "../event-bus"

export default {
    name:"SubjectAdd",
    data(){
        return{
            subjectForm:{}
        }
    },
    methods:{
        subjectsubmit(){
            fetch("http://localhost:3000/subjects",{
            method:"POST",
            headers: {"content-type": "application.json"},
            body: JSON.stringify(this.subjectForm)
            })
            .then(() => {
                Eventbus.emit("subjectchange", {message:'add'})
            })
        }
    }
}
</script>

<style scoped>
    *{
        margin: 3px;
        color: rgb(132, 132, 132);
    }
    .form{
        background-color: #ffffff;
        margin-top: 15px;
        border-radius: 5px;
    }
    .addBut {
        padding: 8px 15px;
        border-radius: 5px;
        border: none;
        cursor: pointer;
        transition: 0.3s;
        font-weight: bold;
        color: white;
        background-color: #198900;
    }
    .addBut:hover {
        background-color: #136d00;
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
</style>