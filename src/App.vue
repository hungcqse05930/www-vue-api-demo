<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <button @click="getPosts">
      <h1>{{ cai_gi_day.hola }}</h1>
    </button>
    <div id="products">
      <!-- Vòng for này sẽ chạy hết products để lấy các product ra -->
      <div class="product" v-for="product in products" v-bind:key="product.id">
        <!-- Chỗ này để ánh xạ các thuộc tính trong mỗi item của products -->
        <h1>{{ product.title }}</h1>
        <hr />
        <strong>{{ product.body }}</strong>
        <p>{{ product.userId }}</p>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  data() {
    return {
      // giá trị được lấy về sẽ đưa vào products
      // Nó là kiểu dữ liệu của products
      products: Object, // hoặc kiểu data, hoặc là giá trị gì đấy luôn ạ
      // vì javascript tự hiểu giá trị nào thì mang kiểu dữ liệu gì
      // hồi nãy chị comment cả "products: Object" nên nó không biết products là cái nào
      // number_of_products: 3,
      //welcome: 'Hello there!',
      // cai_gi_day: {
      //   "id": 2,
      //   "hola": "dăidaijwife",
      //   "OK": 2.94
      // }
      // theo em thì việc khai báo luôn những biến gì cần sử dụng ở đây là để coder dễ nhìn dễ hiểu
      // hơn thôi, mục tiêu của Vue là thế :>
      // có thể nói là vậy ạ 
    };
  },
  // created là khi component Vue được tạo ra nó sẽ làm gì ạ
  // khi mới vào trang trên browser chị thấy nó load luôn content đó
  // chính là cái này ạ
  // có khi là không cần ạ :)) em sẽ lấy thẳng hàm ở dưới dùng luôn
  created: function () {
    this.getPosts();
  },
  methods: {
    getPosts() {
      let id = Math.floor(Math.random() * 10);

      // fetch là 1 promise -> gửi request đến url trong fetch
      fetch(`https://jsonplaceholder.typicode.com/posts?userId=${id}`)
        // sau đó, khi nhận được response, chuyển response về dạng json
        .then((response) => response.json())
        //  chuyển về json xong thì thực hiện phun data vào trong Vue
        .then((json) => {
          // trong trường hợp không có dữ liệu gì
          if (Object.keys(json).length == 0) {
            // cho products một cái giá trị gì đó để hiển thị cho người dùng biết không có gì
            this.products = {
              title: "No records found",
              body: "Please choose another user",
              userId: "--",
            };
          } else {
            // products là biến đã được khai báo để lưu dữ liệu
            // đây là khi bình thường mình có dữ liệu gì đó thì sẽ thế này ạ
            // hết rồi chị ơi
            this.products = json;
            // this.welcome = "Hedfsdllo there!";
            // // ngay lúc này ạ
            // // em cũng không biết giải thích sao ;))
            // this.cai_gi_day = {
            //   id: 2,
            //   hola: "dăidaijwife",
            //   OK: 2.94,
            // };
          }
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
