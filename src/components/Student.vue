<template>
    <div class="studentBOX">
        
        <!--แสดงรูปนิสิต-->
        <img class="stuImg" :src="andyImg" width="250">
        <img class="stuImg" :src="andyImg2" width="250">
        

        <div class="stuInfo">

            <!--แสดงรายละเอียดนิสิต-->
            <div class="header">
                <h1 class="headerCore">{{Student.studentname}}</h1>
            </div>
            <div class="info">
                <h3>รหัสนิสิต: {{Student.studentID}}</h3>
                <h3>สาขา: {{Student.major}}</h3>
                <h3>โรงเรียน: {{Student.school}}</h3>
            </div>

        </div>
        
    </div>
</template>

<script>
import { Eventbus } from '@/event-bus'

export default {
    name:"Student",
    data(){
        return{

            Student:{},

            andyImg:"https://scontent.futp2-1.fna.fbcdn.net/v/t1.15752-9/486762790_3936435076606685_2555464959539703572_n.jpg?_nc_cat=106&ccb=1-7&_nc_sid=9f807c&_nc_eui2=AeGv-I8Aiwd9n7IfvXJw1HWg02GNxx6XUvHTYY3HHpdS8Wz8A6Kah7IEJY3kV1SidEbGlZ9PTvWyMLy45KhfVyNN&_nc_ohc=JA_s8laWvOMQ7kNvgHmO3c6&_nc_oc=Adltr5zgHvgZqhZ_w_jO5BK5h95u-iITVauaPJ9ed8AIyfE8_8GS7vi_yInwJUVM9mPk8Njxv2HdLAj8_ecf4eyy&_nc_zt=23&_nc_ht=scontent.futp2-1.fna&oh=03_Q7cD1wGj24pIxlR0FomdP5N0CB9OmBR4BuB-InrzAcTIwEWBCA&oe=680F0E36",
            andyImg2:"https://scontent.futp2-1.fna.fbcdn.net/v/t1.15752-9/486380050_991128539657022_6890549791243664050_n.jpg?_nc_cat=100&ccb=1-7&_nc_sid=9f807c&_nc_eui2=AeEVzVVy6Fsw2FLIiWAuVNxzD0BJIpdysY0PQEkil3KxjYfks4M92dAk3fsPet-F2KE8cyZeLUM8iGgIz-Mw_Y_2&_nc_ohc=xJAgx7p0ZZAQ7kNvgEmDkG3&_nc_oc=AdlXlhDaIFfFSPNDRsiCmd0RkNUoGkXPeu8lxFjZDQOcTGE9H688GHx9f8Dcqnmb7tFSN79horeKdAkkYg8Mg5TQ&_nc_zt=23&_nc_ht=scontent.futp2-1.fna&oh=03_Q7cD1wFQUspguqIcMgnR7L2IX0hli4w4nfv0mi_0BXT1aU-X_Q&oe=6814A183"
        }
    },
    methods:{
        readStudent(){
            fetch("http://localhost:3000/Student")
            .then(res => res.json())
            .then(data => {
                this.Student = data
            })
            .catch(err => console.log(err.message))
        }
    },
    mounted(){

        this.readStudent()

        Eventbus.on('studentchange',() => {
            this.readStudent()
        })

        
    }
}
</script>

<style scoped>
    .studentBOX{
        display: flex;
        background-color: #222;
    }
    .stuInfo{
        border-radius: 10px;
        background-color: #1a1a1a;
        margin: 25px;
    }
    .stuImg{
        margin-top: 14px;
        margin-left: 14px;
        margin-bottom: 14px;
    }
    .header{
        background-color: #000000;
        border-radius: 10px;
        margin: 5px;
    }
    .headerCore{
        align-items: center;
        margin-left: 5%;
    }
    .info{
        margin: 7px;
    }
    @media (max-width: 1258px){
        .studentBOX{
            margin: 50px;
            width: 920px;
        }
    }
</style>