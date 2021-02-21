<template>
  <div id="app">
      <draggable @start="test($event)" class="test">
        <p
          v-for="user in filteredUsers"
          :key="user.id"
          class="demo"
          ghost-class="ghost"
          @dragstart="dragstartEvt($event)"
          @dragend="dragendEvt($event)"
          :id="user.name"
        >
          {{ user.name }}
        </p>
      </draggable>
  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
  layout: "search",
  components: {
    draggable,
  },
  data: function () {
    return {
      results: [],
      keyword: "",
    };
  },
  asyncData() {
    const users = require(`~/assets/sample.json`);
    return {
      users,
    };
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

      return users;
    },
  },
  methods: {
    test(event) {
      var dt = event.dataTransfer;
      console.log(event);
      //   dt.setData("Text", event.target.id);
      //   dt.setData("text/plain", event.target.id);
      //   var image = new Image();
      //   image.src = "@/assets/example.png";
      //   dt.setDragImage(image, image.width / 2, image.height / 2);
      //   debugger;
    },
    dragstartEvt(event) {
    //   var target = event.target;
    //   target.style.cursor = "grabbing";
    //   var dt = event.dataTransfer;
    //   dt.setData("Text", event.target.id);
    //   dt.setData("text/plain", event.target.id);
    //   var image = new Image();
    //   image.src = require("@/assets/example.png");
    //   dt.setDragImage(image, image.width / 2, image.height / 2);
    //   dt.effectAllowed = "none";
    //   dt.dropEffect = "none";
    //   console.log(event);
    // event.dataTransfer.setData(format, 'Dragme');
    event.dataTransfer.effectAllowed = "none";
    var target = event.target;
    target.style.backgroundColor = 'blue';
    target.style.cursor = 'move'; // You can do this or use a css class to change the cursor
      //   debugger;
    },
    dragendEvt(event) {
      var target = event.target;
      target.style.backgroundColor = "";
      target.style.cursor = "default"; // Reset cursor
      return true;
    },
  },
};
</script>

<style>
.inputText {
  width: 80%;
  padding: 10px;
  margin: 0 auto;
  display: block;
}
p{
    cursor: grabbing !important;
}
.test{
    cursor: grabbing kit!important;

}
/* p {
  cursor: pointer;
}
p:active {
  cursor: none;
} */
</style>
