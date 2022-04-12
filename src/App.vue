<template>
  <section>
    <h1>Hello world</h1>
    <form @submit.prevent="submitForm">
    <!--ref dom element-->
    ป้อนชื่อเล่น : <input type="text" ref="nicknameEl" />
    <button type="submit">Submit</button>
    </form>
    <!-- ตัวอย่่าง การใช้งาน computed -->
    ป้อนฐานเงินเดือน หรือกดปุ่มเพิ่มเงินเดือน: <input type="text" @input="onSalaryInput" :value="salary" /> <br />
    <button @click="addSalary(5000)">เพิ่มเงินเดือน</button>
    <!-- สิ้นสุดตัวอย่่าง การใช้งาน computed -->


    {{firstName}} {{lastName}}<br /> อายุ ::{{age}} <br />
    {{800 + 200}} <br /><br />
    {{position}}
    <div v-html="position"></div>
    <div>jnterpolation</div>
    {{getFullName}}
    <img :src="picture" :width="size" :height="size" ref="imageURL" />
    facebook: <a :href="social">Link</a> <br />
    ชื่อเล่น : {{nickName}} <br />
    ฐานเงินเดือน :: {{salary}}
    ตำแหน่ง :: {{computedSalaryRole}}
    <div>
      <p v-if="hobby.length === 0">
        ไม่มีงานอดิเรก
      </p>
      <div v-else>
        งานอดิเรก
        <ul>
          <li>{{hobby[0]}}</li>
          <li>{{hobby[1]}}</li>
          <li>{{hobby[2]}}</li>
        </ul>

        V-for (Array)
        <ul>
          <!--v-bind:key="hobby" or :key="hobby"-->
          <li v-for="(item, index) in hobby" v-bind:key="index">{{index + 1}} {{item}}</li>
        </ul>
      </div>
    </div>
    <h2>Method1: {{getRandomByMethod()}}</h2>
    <h2>Method2: {{getRandomByMethod()}}</h2>
    <h2>Method3: {{getRandomByMethod()}}</h2>
    <h2>Method Computed1: {{getRandomByComputed}} </h2>
    <h2>Method Computed2: {{getRandomByComputed}} </h2>
    <h2>Method Computed3: {{getRandomByComputed}} </h2>

    <button @click="toggleVisible">{{isVisible ? 'ซ่อน' : 'แสดง'}}</button>
    สถานะ :: {{isVisible}}
    
    <article v-show="isVisible">
      <p> ข้อมูลพื้นฐาน </p>
      <ul>
        <li>เพศ {{general.gender}}</li>
        <li>น้ำหนัก {{general.weight}}</li>
        <li>สถานะ {{general.status}}</li>
      </ul>

      <div>
        V-for (Object)
        <ul>
          <li v-for="(item, key) in general" :key="key">{{key}} -> {{item}}</li>
        </ul>
      </div>

      <button v-on:click="showData">คลิกเพื่อดูข้อมูล แบบ v-on</button>
      <button @click="showData">คลิกเพื่อดูข้อมูล แบบ @click (ลดรูป)</button>
      <button @click="increment(10)">เพิ่มอายุ</button>
      <button @click="decrement">ลดอายุ</button>
      <!-- middle left right --- mouse modifier --->
      <button @click.middle="decrement">ลดอายุ โดยการคลิกเมาส์กลาง</button>
    </article>
  </section>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      firstName: 'Test',
      lastName: 'User',
      nickName: "",
      age: 15,
      position: '<h1>Full Stack Developer</h1>',
      picture: 'https://image.shutterstock.com/image-vector/user-icon-vector-260nw-421041541.jpg',
      size: 50,
      social: "https://www.facebook.com/johndoe",
      hobby: ['เขียนโค้ด', 'อ่านหนังสือ', 'เรียนออนไลน์', 'ท่องเน็ต'],
      general: {
        status: 'single',
        gender: 'man',
        weight: 70.4
      },
      isVisible: false,
      salary: 10000
    }
  },
  methods: {
    getLastName() {
      return this.lastName
    },
    showData() {
      alert(this.firstName + ' ' + this.lastName + ' ' + this.age)
    },
    increment(value) {
      this.age+=value
    },
    decrement() {
      this.age--
    },
    setNickName(event) {
      this.nickName = event.target.value
    },
    submitForm() {
      // e.preventDefault() คงสภาพไม่ให้มัน refresh
      alert("บันทึกชื่อเล่นเรียบร้อย")
      this.nickName = this.$refs.nicknameEl.value
    },
    toggleVisible() {
      this.isVisible = !this.isVisible
    },
    getRandomByMethod() {
      return Math.random()
    },
    onSalaryInput(e) {
      this.salary = e.target.value
    },
    addSalary(value) {
      this.salary += value
    }
  },
  computed: {
    getFullName() {
      return this.firstName + ' ' + this.lastName
    },
    getRandomByComputed() {
      return Math.random()
    },
    computedSalaryRole() {
      return this.salary > 20000 ? 'Senior' : 'Junior'
    }
  },
  watch: {
    salary(value) {
      console.log('มีการเปลี่ยนแปลงค่า salary -> ', value)
      if (value > 50000) {
        alert('เงินเดือนไม่ควรเกิน 50000 บาทค่ะ')
        setTimeout(() => {
          this.salary = 50000
        }, 100)
      }
    }
  }
}
</script>

<style>

</style>
