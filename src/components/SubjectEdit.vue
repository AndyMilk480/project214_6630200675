<template>
    <div class="subEdit">
        <!--แบบฟอร์มแก้ไขวิชา-->
        <form id="SubjectEdit" @submit.prevent="editSub">
            <label for="id">รหัสวิชา</label>
            <input type="text" id="id" v-model="editform.subjectID">

            <label for="name">ชื่อวิชา</label>
            <input type="text" id="name" v-model="editform.subjectname"><br>

            <label for="credit">หน่วยกิต</label>
            <input type="number" id="credit" v-model="editform.credit">

            <label for="grade">เกรด</label>
            <input type="text" id="grade" v-model="editform.grade"><br>

            <button class="editBut" type="submit">Submit</button>

        </form>
    </div>
</template>

<script>
import {Eventbus} from "../event-bus"
export default {
    name:"SubjectEdit",
    props:["oldData"],
    data(){
        return{
            editform:{}
        }
    },
    methods:{
        editSub(){
            fetch(`http://localhost:3000/subjects/${this.oldData}`,{
                method:"PATCH",
                headers: {"content-type": "application.json"},
                body: JSON.stringify(this.editform)
            })
            .then(() => {
                Eventbus.emit("subjectchange", {message:'edit'})
            })
        }
    }

}
</script>

<style scoped>
    .subEdit{
        background-color: rgb(255, 255, 255);
        margin: 10px;
        border: 1px solid rgb(192, 192, 192);
        border-radius: 5px;
    }
    *{
        margin: 3px;
        color: rgb(132, 132, 132);
    }
    .editBut {
        padding: 8px 15px;
        border-radius: 5px;
        border: none;
        cursor: pointer;
        transition: 0.3s;
        font-weight: bold;
        color: white;
        background-color: #ff9800;
    }
    .editBut:hover {
        background-color: #e68900;
    }
    input{
        border-radius: 4px;
        border: 1px solid rgb(192, 192, 192);
    }
    input:hover{
        border: 1px solid rgb(116, 197, 255);
    }
</style>