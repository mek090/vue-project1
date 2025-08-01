<template>
    <div>
        <img :src="picture" alt="Profile" />
        <button @click="toggleVisible">
            {{ isvisible ? 'ซ่อนข้อมูล' : 'แสดงข้อมูล' }}
        </button>

        <div v-show="isvisible">
            <h1>{{ fullName }}</h1>
            <h2>Method1 : {{ getRandomByMethod() }}</h2>
            <h2>Method2 : {{ getRandomByMethod() }}</h2>
            <hr />
            <!-- <h2>computed : {{ getRandomByComputed() }}</h2> -->
            <!-- <h2>Computed1 : {{ getRandomComputed() }}</h2> -->
            <!-- <h2>Computed2 : {{ getRandomComputed() }}</h2> -->
            <form @submit.prevent="submitForm">
                <label>nickname</label>
                <input type="text" :value="nickname" @input="setNickname" ref="nicknameInput" />
                <button type="submit">save</button>
            </form>

            <h2> เงินเดือน : {{ salary }} บาท</h2>
            <h2> ตำแหน่งงาน : {{ getDepartment }}</h2>
            <button @click="addSalary(5000)">เพิ่มเงินเดือน</button>
            <button @click="reduceSalary(5000)">ลดเงินเดือน</button>
            <br>

            <label>ชื่อเล่น</label>
            <p v-if="nickname">ชื่อเล่น: {{ nickname }}</p>
            <p><i>1234 Test St, Test City, TC 12345</i></p>

            <div>
                <a :href="picture" target="_blank">Instagram</a>
                <a href="#">Twitter</a>
                <a href="#">Github</a>
            </div>

            <div>
                <h2>ข้อมูลทั่วไป</h2>
                <ul>
                    <li v-for="(value, key) in general" :key="key">
                        <strong>{{ key }} :</strong> {{ value }}
                    </li>
                </ul>
            </div>

            <h1 v-if="hobbyList.length === 0">ไม่มีงานอดิเรก</h1>
            <div v-else>
                <h2>งานอดิเรก</h2>
                <ul>
                    <li v-for="(item, index) in hobbyList" :key="index">
                        {{ index + 1 }} - {{ item }}
                    </li>
                </ul>
            </div>

            <button @click="showData">กดเพื่อดูข้อมูล</button>
        </div>
    </div>
</template>

<script>
import { set } from 'mongoose';


export default {
    data() {
        return {
            firstName: 'MKE',
            lastName: 'Eiei',
            nickname: '',
            picture:
                'https://www.shutterstock.com/image-photo/handsome-young-man-taking-selfie-260nw-2430940187.jpg',
            hobbyList: ['เล่นเกม', 'อ่านหนังสือ', 'ดูหนัง', 'ท่องเที่ยว'],
            general: {
                gender: 'ชาย',
                age: 20,
                height: 170,
                weight: 70,
                status: false,
            },
            isvisible: true,
            salary: 20000,
        };
    },
    computed: {
        fullName() {
            return `${this.firstName} ${this.lastName}`;
        },
        getRandomComputed() {
            return Math.random();
        },
        getIncome() {
            return this.salary * 12;
        },
        getDepartment() {
            return this.salary >= 35000 ? 'Programmer' : 'IT Support';
        },
    },
    methods: {
        incrementAge(val) {
            this.general.age += val;
        },
        decrementAge(val) {
            this.general.age = Math.max(0, this.general.age - val);
        },
        showData() {
            alert(`ชื่อเต็ม: ${this.fullName}`);
        },
        setNickname(event) {
            this.nickname = event.target.value;
        },
        submitForm() {
            const nicknameInputValue = this.$refs.nicknameInput.value;
            alert(`Nickname saved: ${nicknameInputValue}`);
            console.log('Value from ref:', nicknameInputValue);
        },
        toggleVisible() {
            this.isvisible = !this.isvisible;
        },
        getRandomByMethod() {
            return Math.random();
        },
        addSalary(amount) {
            this.salary += amount;
        },
        reduceSalary(amount) {
            this.salary = Math.max(0, this.salary - amount);
        },
    },
    watch: {
        salary(value) {
              if (value > 50000) {
                // this.salary1 = 50000;
                alert(`เงินเดือนไม่ควรเกิน 50000`);
                setTimeout(() => {
                    this.salary = 50000;
                }, 100);
            }
        },
        nickname(newVal) {
            console.log('Nickname changed:', newVal);
        },
    },
};
</script>

<style scoped>
/* ไม่ใช้ CSS */
</style>
