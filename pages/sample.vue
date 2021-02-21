<template>
  <div>
    <h1>
      assset API
    </h1>
    <h2>Users</h2>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.id }} - {{ user.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  asyncData() {
    const users = require(`~/assets/user.json`)
    return {
      users
    }
  }
}
</script>