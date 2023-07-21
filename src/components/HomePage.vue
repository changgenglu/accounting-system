<template>
  <div class="container w-50">
    <div class="row">
      <!-- <h1>多人帳務系統</h1> -->
      <div class="input-group pb-4 col-12">
        <input type="text" class="form-control " v-model="newUsername" placeholder="輸入使用者名稱">
        <button class="btn btn-success" @click="addUser">新增使用者</button>
      </div>
      <div v-for="user in users" :key="user.id" class="col-6 p-1">
        <div class="card">
          <div class="card-header">
            <p class="h3">{{ user.name }}</p>
          </div>
          <div class="card-body">
            <div class="input-group mb-3">
              <input class="form-control col-6" type="text" v-model.lazy="expenseItem" placeholder="支出項目">
              <input class="form-control col-4" type="number" v-model.lazy="expenseAmount" placeholder="$">
              <button class="btn btn-success col-2" @click="addExpense(user.id)">+</button>
            </div>
            <div v-for="(expense, index) in user.expenses" :key="index" class="mb-2">
              <div class="input-group">
                <div class="col-6 input-group-text">{{ expense.item }}</div>
                <div class="col-4 form-control">{{ expense.amount }}</div>
                <button class="btn btn-danger col-2"
                  @click="deleteExpense(user.id, expense.item, expense.amount)">-</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="d-grid gap-2 col-6 mx-auto mt-4">
      <button class="btn btn-lg btn-success">共計：{{ totalAmount }} 元</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  data() {
    return {
      newUsername: "", // 新增使用者的名稱
      users: [], // 使用者清單陣列
      activeUserId: null, // 目前正在編輯支出的使用者 ID
      expenseItem: '', // 支出項目輸入值
      expenseAmount: null, // 支出金額輸入值s
      totalAmount: 0,
    }
  },
  watch: {
    expenseAmount: function () {
      let totalAmount = 0;
      for (const user of this.users) {
        if (user.expenses) {
          for (const expense of user.expenses) {
            totalAmount += expense.amount;
          }
        }
      }
      this.totalAmount = totalAmount;
    }
  },
  methods: {
    addUser() {
      const username = this.newUsername.trim();
      if (username !== "") {
        const user = this.users.find((user) => user.name === username);

        if (typeof user === "undefined") {
          const user = { id: this.users.length + 1, name: username };
          this.users.push(user);
        } else {
          alert("User already exists: " + username)
        }
        this.newUsername = "";
      }
    },
    showInput(userId) {
      // 切換顯示輸入框的使用者 ID
      this.activeUserId = userId;
      // 清空輸入欄位
      this.expenseItem = '';
      this.expenseAmount = null;
    },
    addExpense(userId) {
      const item = this.expenseItem.trim();
      const amount = parseFloat(this.expenseAmount);

      if (item !== '' && !isNaN(amount) && amount > 0) {
        // 找到目前正在編輯支出的使用者
        const user = this.users.find((user) => user.id === userId);

        // 建立支出物件並加入使用者的支出清單
        const expense = { item: item, amount: amount };
        if (!user.expenses) {
          user.expenses = [];
        }
        user.expenses.push(expense);

        // 清空輸入欄位
        this.expenseItem = '';
        this.expenseAmount = null;
      }
    },
    deleteExpense(userId, item, amount) {
      const user = this.users.find((user) => user.id === userId);
      const expense = user.expenses.find((expense) => expense.item === item && expense.amount === amount);
      if (expense) {
        // delete expense
        user.expenses.splice(expense, 1);
      }
    }
  },
}
</script>

<style scoped></style>
