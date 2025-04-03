<template>
  <div class="container ">
    <br><br><br>

    <div class="flex flex-col md:flex-row items-center md:items-start">

      <div>
        <br>
        <h3 class="text-2xl font-semibold text-gray-700 mb-3" align="center" style="color: #081F5C;"> .•*´¨`*•.¸¸.•*´¨`*•.¸¸.•*     ข้อมูลนิสิต     .•*´¨`*•.¸¸.•*´¨`*•.¸¸.•*</h3><br><br>
        <img src="C:\Users\User\OneDrive\Desktop\project_finalY2\project214_6630200713\data\255176_0.jpg"
          class="rounded float-start shadow-lg w-20 h-10 mb-5 md:mb-0 md:mr-10 mt-20" height="280px" />
        <br><br>
        <div class="shadow-lg rounded p-3  ml-5 " align="center" style="background-color: #B9CBE1; border-radius: 5px;">
          <p><strong text-color=#F5EFEB>ชื่อ:</strong> {{ name }} <strong>นามสกุล:</strong> {{ lastname }}</p>
          <p><strong>รหัสนิสิต:</strong> {{ id }}</p>
          <p><strong>สาขา:</strong> {{ major }}</p>
          <p><strong>โรงเรียนเดิม:</strong> {{ school }}</p>
        </div>
      </div>

      <div class="mt-2 " align="right">
        <button class="mt-4 mr-10 px-4 py-2 bg-blue-500 text-black rounded shadow hover:bg-blue-600"
          @click="setcData" style="background-color: #DDD7E5;">แก้ไขข้อมูล</button>
      </div>

    </div>

    <div v-show="showd" class="mt-5 p-5 bg-gray-100 rounded-lg shadow" style="background-color: #FFE7E7;">
      <h3 class="text-lg font-semibold text-gray-700">.•° ✿ °•. แก้ไขข้อมูล .•° ✿ °•.</h3>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div>
          <label>ชื่อ:</label>
          <input type="text" v-model="name_c" class="input-field" />
          <button class="btn-confirm" @click="setname(name_c)">ยืนยัน</button>
        </div>
        <div>
          <label>นามสกุล:</label>
          <input type="text" v-model="name_l" class="input-field" />
          <button class="btn-confirm" @click="setlast(name_l)">ยืนยัน</button>
        </div>
        <div>
          <label>รหัสนิสิต:</label>
          <input type="text" v-model="name_id" class="input-field" />
          <button class="btn-confirm" @click="setID(name_id)">ยืนยัน</button>
        </div>
        <div>
          <label>สาขาวิชา:</label>

          <select class="input-field" v-model="major" @change="setMa(major)">
            <option value="Com-sci">Com-sci</option>
            <option value="Chame-sci">Chame-sci</option>
            <option value="DST">DST</option>
            <option value="DAAS">DAAS</option>
            <option value="Envi">Envi</option>
          </select>
        </div>
        <div>
          <label>โรงเรียนเดิม:</label>
          <input type="text" v-model="name_sc" class="input-field" />
          <button class="btn-confirm" @click="setsc(name_sc)">ยืนยัน</button>
        </div>
      </div>
    </div>
    <br>
    <h3 class="text-center text-xl font-semibold text-gray-700 mt-5">》* 。 • ˚ ˚ ˛ * 。 รายวิชาที่ลงเรียน˚ ˚ ˛ * 。° 。 • ˚《</h3>
    <div class="flex justify-center space-x-3 mt-3" style="display: flex; justify-content: left; align-items: center; gap: 10px;">
      <button class="btn-tab" @click="setshows" >แสดง</button>
      <button class="btn-tab" @click="setAdd">เพิ่ม</button>

    </div>

    <div v-show="showsub" class="mt-4">
      <SubList />
    </div>
    <div v-show="show_add" class="mt-4">
      <Subadd />
    </div>

    <div style="display: flex; justify-content: center; align-items: center; gap: 50px;">
      <img src="C:\Users\User\OneDrive\Desktop\project_finalY2\project214_6630200713\data\255191.jpg"
        class="rounded float-start shadow-lg" height="400px" />
      <img src="C:\Users\User\OneDrive\Desktop\project_finalY2\project214_6630200713\data\255203.jpg"
        class="rounded float-start shadow-lg" height="400px" />
    </div>
    <br><br>
  </div>

</template>



<script>

import SubList from './components/SubList.vue';
import Subadd from './components/Subadd.vue';
export default {
  name: "App",
  props: ['id'],
  components: {
    SubList,
    Subadd
  },
  data() {
    return {
      ///ตัวแปรที่ใช้
      name: "รสิตา",
      lastname: "รัตนอมรกุลชัย",
      id: "6630200713",
      major: "com-sci",
      school: "อัสสัมชัญศึกษา",
      showd: false,
      showsub: true,
      name_c: null,
      name_l: null,
      name_id: null,
      show_add: false,
      student: [],
    };
  },
  methods: {
    setname(n) {
      this.name = n;
    },
    setcData() {
      this.showd = !this.showd;
    },
    setlast(n) {
      this.lastname = n;
    },
    setID(id) {
      this.id = id;
    },
    setMa(ma) {
      this.major = ma;
    },
    setsc(sc) {
      this.school = sc;
    },
    setAdd() {
      this.show_add = !this.show_add;
      this.showsub = false;
    },
    setshows() {
      this.showsub = true;
      this.show_add = false;
    }
  },

};
</script>
<style scoped>
.input-field {
  width: 100%;
  padding: 8px;
  border: 1px solid #B3B792;
  border-radius: 5px;
  outline: none;
  transition: border-color 0.3s ease-in-out;
  font-family: 'Poppins', sans-serif;
}

.input-field:focus {
  border-color: #809671;
  font-family: 'Poppins', sans-serif;
}

.btn-confirm {
  margin-top: 5px;
  padding: 5px 10px;
  background-color: #ADB8D6;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
  font-family: 'Poppins', sans-serif;
}

.btn-confirm:hover {
  background-color: #B38B60;
  font-family: 'Poppins', sans-serif;
}

.btn-tab {
  padding: 8px 16px;
  background-color: #f2f0de; 
  color: #0d9277;

  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
  font-family: 'Poppins', sans-serif;
}

.btn-tab:hover {
  background-color: #a5eee9;
}

.container {
  background-color: #FFFBF2;
  min-height: 100vh;
}
</style>
