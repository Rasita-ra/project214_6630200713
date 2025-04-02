<template>

    <div class="card w-100 mb-7">
        <div class="card-body" style="background-color: #fff9c7;" >
            <form @submit.prevent="handleSubmit()">
            <div>
            <p>ชื่อรายวิชา</p>
            <input type="text" v-model.trim="sub.subname" />
            <p>รหัสวิชา</p>
            <input type="text" v-model.trim="sub.id" />
            <p>หน่วยกิต</p>
            <input type="text" v-model.trim="sub.credit" />
            <p>ผลการเรียน</p>
            <input type="text" v-model.trim="sub.gread" /><br><br>
            </div>
            <div class="mt-2 d-flex align-items-center">
                <button type="submit" class="btn btn-primary mt-10" style="background-color: #feb737; color:white;" >
                    ยืนยันการแก้ไข
                </button>
            </div>
            </form>
        </div>
        <div class="alert alert-success mt-s" v-if="editOK">
            บันทึกข้อมูล{{ sub.subname }} สำเร็จ
        </div>
        <div class="alert alart-danger mt-s" v-if="editErr">
            {{ editMessage }}
        </div>
    </div>
</template>

<script>
import {EventBus} from "../event-bus"
export default {
    name:"Subedit",
    props:['id'],
    data(){
        return{
            sub:{
                id:null,
                subname:null,
                credit:null,
                gread:null,
            },
            editOK:false,
            editErr:false,
            editMessage:null,
            
        }
    },
    methods: {
        handleSubmit() {
             ///let subjects = {
                ///id: this.sub.id,
                //subname: this.sub.subname,
                //credit: this.sub.credit,
               // gread: this.sub.gread,
            ///};
            fetch(`http://localhost:3000/subjects/${this.id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(this.sub),
            })
            .then(()=>{
                this.editOK=true;
                console.log("")
                this.editMessage="แก้ไขสำเร็จ"
                EventBus.emit("stdChange",{messege:'edit'})
            })
            .catch((err)=>{
            this.editErr=true;
            this.editOK=false;
            this.editMessage=err;
            }
        )
        }
    },
    mounte (){
        fetch(`http://localhost:3000/subjects/${this.id}`)
                .then(res => res.json())
                .then(data => this.sub = data)
                .catch(err => console.error(err.massege))

    }
}
</script>

<style></style>