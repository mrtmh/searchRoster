<template>
  <div id="app">
    <input type="text" v-model="keyword" placeholder="検索したい方の名前を入力してください" class="inputText" />
    <table>
      <tr v-for="user in filteredUsers" :key="user.id">
        <td v-text="user.id"></td>
        <td v-text="user.name"></td>
        <td v-text="user.email"></td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  layout: "search",
  data: function () {
    return {
      results: [],
      keyword: "",
    };
  },
  asyncData() {
    const users = require(`~/assets/sample.json`)
    return {
      users
    }
  },
  computed: {
    /*
    検索機能
    */
    filteredUsers: function () {
      var users = [];

      for (var i in this.users) {
        var user = this.users[i];

        if (user.name.indexOf(this.keyword) !== -1) {
          users.push(user);
        }
      }
      for (var i in this.users) {
        var user = this.users[i];

        if (user.email.indexOf(this.keyword) !== -1) {
          users.push(user);
        }
      }

      return users;
    },
  },
};
</script>

<style>
.inputText{
  width: 80%;
  padding: 10px;
  margin: 0 auto;
  display: block;
}
table {
  padding-top: 40px;
  width: 80%;
  margin: 0 auto;
  color: #333;
}
td{
  padding: 10px;
}
tr:nth-child(2n+1){
  background-color:#efefef;
}
</style>
