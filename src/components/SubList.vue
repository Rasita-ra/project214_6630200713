<template>

    <div class="contriner" align="center">
        <li class="list-group-item" v-for="(sub, id) in Subjects" :key='id' align="center">
            <div class="card border-dark mb-3" width="50">

                <div class="card-body" style="background-color: #bcd7db;">
                    <pre class="card-title">ชื่อวิชา {{ sub.subname }}    รหัสวิชา {{ sub.id }}</pre>

                    <pre> หน่วยกิต : {{ sub.credit }}    ผลการเรียน : {{ sub.gread }}</pre>
                    <button class="btn btn-primary mx-2" @click="delDetail(sub.id)" style="background-color: #163550; color: #e9f3ff;">ลบข้อมูล</button>

                    <div class="btn-group mb-2 mt-2" style="width: 5100 px; ">
                        <button type="button" class="btn  btn dropdown-toggle " data-bs-toggle="dropdown"
                            aria-expanded="false" style="background-color: #163550; color: #e9f3ff;">แก้ไขข้อมูล
                        </button>
                        <ul class="dropdown-menu">
                            <li><a class="dropdown-item" href="#">
                                    <Subedit :id="sub.id" />
                                </a></li>

                        </ul>
                    </div>
                </div>
            </div>
        </li>
    </div>



</template>

<script>

import { EventBus } from "../event-bus"
import Subadd from './Subadd.vue';
import Subedit from "./Subedit.vue";
export default {
    name: "SubList",
    components: {
        Subadd, Subedit
    },
    props: ['id'],
    data() {
        return {
            Subjects: [
            ],
            showadd: false,
            editshow: false
        }
    },
    mounted() {
        this.getData()
        EventBus.on('stdchange', (data) => {
            console.log('มีการเปลี่ยนแปลง----> ${data.message}')
            this.getData()
        })
    },
    methods: {
        setAdd() {
            this.showadd = !this.showadd;
        },
        handleSubmit() {
            let subjects = {
                id: this.sub.id,
                subname: this.sub.subname,
                credit: this.sub.credit,
                gread: this.sub.gread,
            };
            fetch(`http://localhost:3000/subjects`, {
                method: "POST",
                headers: { "Content-Type": "appcation/json" },
                body: JSON.stringgify(subjects),
            })
        },
        getData() {
            fetch(`http://localhost:3000/subjects`)
                .then(res => res.json())
                .then(data => this.Subjects = data)
                .catch(err => console.error(err.massege))
        },
        delDetail(de) {
            if (confirm("ยืนยันการลบข้อมูล")) {
                fetch(`http://localhost:3000/subjects/${de}`, { method: 'DELETE' })
                    .then(() => {
                        EventBus.emit("stdChange", { message: 'delete' })
                    })
                    .catch(err => console.log(err.message))
            }
        }
    }
}
</script>

<style></style>