<template>

    <div class="card w-75 mb-3">
        <div class="card-body" style="background-color: #FFE7E7;">
            <form @submit.prevent="handleSubmit()">
            <h1>เพิ่มรายวิชาที่ลงเรียน</h1><br>
            <div>
            <p>ชื่อรายวิชา :</p>
            <input type="text" v-model.trim="sub.subname" />
            <p>รหัสวิชา :</p>
            <input type="text" v-model.trim="sub.id" />
            <p>หน่วยกิต :</p>
            <input type="text" v-model.trim="sub.credit" />
            <p>ผลการเรียน :</p>
            <input type="text" v-model.trim="sub.gread" /><br><br>
            </div>
            <div class="mt-2 d-flex align-items-center">
                <button type="submit" class="btn btn-primary mt-10" style="background-color: #f8a19f;">
                    ยืนยันการเพิ่ม
                </button>
            </div>
            </form>
        </div>
        <div class="alert alert-success mt-s" v-if="addOK">
            บันทึกข้อมูล{{ sub.subname }} สำเร็จ
        </div>
        <div class="alert alart-danger mt-s" v-if="addErr">
            {{ addMessage }}
        </div>
    </div>
</template>

<script>
import {EventBus} from "../event-bus"
export default {
    name:"Subadd",
    props:['id'],
    data(){
        return{
            sub:{
                id:null,
                subname:null,
                credit:null,
                gread:null,
            },
            addOK:false,
            addErr:false,
            addMessage:null,
            
        }
    },
    methods: {
        handleSubmit() {
            let subjects = {
                id: this.sub.id,
                subname: this.sub.subname,
                credit: this.sub.credit,
                gread: this.sub.gread,
            };
            fetch(`http://localhost:3000/subjects`, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(subjects),
            })
            .then(()=>{
                this.addOK=true;
                console.log("")
                EventBus.emit("stdChange",{messege:'add'})
            })
            .catch((err)=>{
            this.addErr=true;
            this.addOK=false;
            this.addMessage=err;
            }
        )
        }
    }
}
</script>

<style></style>