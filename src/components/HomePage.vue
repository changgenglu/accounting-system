<template>
  <div class="container">
    <h1>多人帳務系統</h1>
    <div>
      <div class="input-group">
        <input type="text" class="form-control " v-model="newUsername" placeholder="輸入使用者名稱">
        <button class="btn btn-success" @click="addUser">新增使用者</button>
      </div>
    </div>
    <div>
      <button class="btn btn-primary " style="margin: 10px;" v-for="user in users" :key="user.id">使用者 ID: {{ user.id }}，名稱: {{ user.name
      }}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      newUsername: "", // 新增使用者的名稱
      users: [], // 使用者清單陣列
    }
  },
  methods: {
    addUser() {
      const username = this.newUsername.trim();

      if (username !== "") {
        // 建立使用者物件並加入使用者清單
        const user = { id: this.users.length + 1, name: username };
        this.users.push(user);

        // 清空輸入欄位
        this.newUsername = "";
      }
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
