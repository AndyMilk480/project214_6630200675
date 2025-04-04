<template>
    <div class="subList">
        <h1>รายละเอียดวิชา</h1>

        <div class="subPice" v-for="(subject, id) in subjects" :key="id">
            <!--แสดงรายละเอียดวิชาทีละวิชา-->
            <div class="subBox">
                <p class="subData">รหัส: {{subject.subjectID}} วิชา: {{subject.subjectname}} หน่วยกิต: {{subject.credit}} เกรด: {{subject.grade}}</p>

                <div class="buttonGroup">
                    <button class="buttonEdit" type="button" @click="editSubject(subject)">Edit</button>
                    <button class="buttonDelete" type="button" @click="deleteSubject(subject.id)">🗑 Delete</button>
                </div>
            </div>

            <!--แก้ไขรายวิชา-->
            <div v-if="subject.active">
                <subject-edit :oldData="subject.id"></subject-edit>
            </div>
        </div>

        <!--เพื่มวืชา-->
        <button class="addButton" type="button" ref="inButton" @click="addSwitch()">+ เพิ่มวิชา</button>
        <div v-if="addSubject == true">
            <subjectAdd></subjectAdd>
        </div>

    </div>
</template>

<script>
import SubjectAdd from './SubjectAdd.vue'
import SubjectEdit from './SubjectEdit.vue'
import {Eventbus} from '../event-bus'

export default {
    name: "Subject",
    components: {
        SubjectAdd,
        SubjectEdit
    },
    data() {
        return {
            subjects: [],
            addSubject: false
        }
    },
    methods: {
        addSwitch() {
            this.addSubject = !this.addSubject

            this.subjects.forEach(subject => {
                subject.active = false
            })
        },
        deleteSubject(row) {
            if (confirm("ยืนยันการลบข้อมูล")) {
                fetch(`http://localhost:3000/subjects/${row}`, { method: 'DELETE' })
                    .then(() => this.getData())
            }
        },
        editSubject(row) {
            if (row.active) {
                row.active = false
            } else {
                this.subjects.forEach(subject => {
                    subject.active = false
                })
                row.active = true
            }
        },
        getData() {
            fetch("http://localhost:3000/subjects")
                .then(res => res.json())
                .then(data => {
                    this.subjects = data
                })
                .catch(err => console.log(err.message))
        },
        handleClickOutside(event){
            const button = this.$refs.inButton;
            if (button && !button.contains(event.target)) {
                this.addSubject = false
            }
        }
    },
    mounted() {
        this.getData()
        Eventbus.on("subjectchange", () => {
            this.getData()
        })
        document.addEventListener("click", this.handleClickOutside);
    },
    unmounted() {
        document.removeEventListener("click", this.handleClickOutside);
    },
}
</script>

<style scoped>
    h1{
        text-align: center;
    }
    .subList {
        background-color: rgb(51, 51, 51);
        margin: 50px auto;
        padding: 20px;
        border-radius: 10px;
        width: 60%;
        box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
        color: white;
        
    }
    .subPice {
        background-color: #222;
        border-radius: 10px;
        padding: 15px;
        margin: 10px 0;
        box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.1);
    }
    .subBox {
        text-align: left;
    }
    .subData {
        color: #333;
        color: #ffffff;
        
    }
    .buttonGroup {
        display: flex;
        gap: 10px;
        margin-top: 10px;
    }
    .buttonEdit, .buttonDelete {
        padding: 8px 15px;
        border-radius: 5px;
        border: none;
        cursor: pointer;
        transition: 0.3s;
        font-weight: bold;
        color: white;
    }
    .buttonEdit {
        background-color: #198900;
    }
    .buttonDelete {
        background-color: #ae2727;
    }
    .buttonEdit:hover {
        background-color: #136d00;
    }
    .buttonDelete:hover {
        background-color: #8b1e1e;
    }
    .addButton {
        margin-left: 15px;
        margin-top: 10px;
        padding: 10px 20px;
        font-size: 16px;
        border-radius: 8px;
        border: none;
        background-color: #ff9800;
        color: white;
        font-weight: bold;
        cursor: pointer;
        transition: 0.3s;
    }
    .addButton:hover {
        background-color: #e68900;
    }
</style>