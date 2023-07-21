<template>
  <div class="container w-50">
    <!-- <h1>多人帳務系統</h1> -->
    <div class="input-group p-5">
      <input type="text" class="form-control " v-model="newUsername" placeholder="輸入使用者名稱">
      <button class="btn btn-success" @click="addUser">新增使用者</button>
    </div>
    <div class="row">
      <div v-for="user in users" :key="user.id" class="card col-6 p-0">
        <div class="card-header">
          <a class="h3" href="#" @click="showInput(user.id)">{{ user.name }}</a>
        </div>
        <div class="card-body">
          <div class="input-group mb-3">
            <input class="form-control" type="text" v-model="expenseItem" placeholder="支出項目">
            <input class="form-control" type="number" v-model="expenseAmount" placeholder="支出金額">
            <button class="btn btn-success" @click="addExpense(user.id)">+</button>
          </div>
          <div v-for="(expense, index) in user.expenses" :key="index" class="mb-2">
            <div class="input-group">
              <div class="input-group-text w-75">{{ expense.item }}</div>
              <div class="form-control">{{ expense.amount }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  data() {
    return {
      newUsername: "", // 新增使用者的名稱
      users: [
        {
          id: 1,
          name: 'ivan',
          expenses: [
            {
              amount: 1234,
              item: "asdf"
            },
            {
              amount: 46798,
              item: "fj.7ir"
            },
          ]
        },
        {
          id: 2,
          name: 'song',
          expenses: [
            {
              amount: 78,
              item: "asdf"
            },
            {
              amount: 1234,
              item: "mlsae"
            },
          ]
        },

      ], // 使用者清單陣列
      activeUserId: null, // 目前正在編輯支出的使用者 ID
      expenseItem: '', // 支出項目輸入值
      expenseAmount: null, // 支出金額輸入值s
    }
  },
  methods: {
    addUser() {
      const username = this.newUsername.trim();
      if (username !== "") {
        const user = { id: this.users.length + 1, name: username };
        this.users.push(user);
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
  },
}
</script>

<style scoped>
.payItem {
  /* position: absolute;
  right: 0;
  top: 0; */
}
</style>
