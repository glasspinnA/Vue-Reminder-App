<template>
  <div class="container">
    <div class="inputSection">
      <input
        type="text"
        placeholder="Enter Reminder"
        autofocus
        @keyup.enter="addItem"
        v-model="inputReminder.content"
      >
      <button @click="addItem">Add</button>
    </div>
    <div class="reminder-container">
      <div class="item-wrapper">
        <transition-group name="reminder-list">
          <div
            v-for="(currentItem) in items"
            v-bind:key="currentItem.keyId"
            class="reminder-list-item"
          >
            <input type="checkbox" @click="toggleState(currentItem)">
            <span v-bind:class="{active: currentItem.status}">{{currentItem.content}}</span>
            <button @click="removeItem(currentItem)">Delete</button>
          </div>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      keyId: 2,
      items: [
        { content: "Julmust", status: false, keyId: 0 },
        { content: "Kakor", status: false, keyId: 1 }
      ],
      inputReminder: { content: undefined, status: false }
    };
  },
  methods: {
    /**
     * Function for adding a new reminder to the list
     */
    addItem: function() {
      if (this.inputReminder.content != undefined) {
        let tempReminderObj = {
          content: this.inputReminder.content,
          status: this.inputReminder.status,
          keyId: this.keyId
        };

        this.items.unshift(tempReminderObj);

        this.inputReminder.content = undefined;
        this.keyId++;
      } else {
        alert("Enter a reminder");
      }
    },
    /**
     * Function for removing a reminder from the list
     */
    removeItem: function(item) {
      if (item.status) {
        this.items.splice(item, 1);
      }
    },
    /**
     * Function for toggle between state for checkboxes
     */
    toggleState: function(item) {
      item.status = !item.status;
    }
  }
};
</script>

<style scoped>
.active {
  text-decoration: line-through;
  color: #8395a7;
}

.container {
  width: 90%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.inputSection {
  text-align: center;
  margin-bottom: 20px;
}

.inputSection input[type="text"] {
  all: none;
  border: 2px solid black;
  border-radius: 20px;
  padding: 10px;
  margin: 10px;
}

.inputSection button {
  all: none;
  border-radius: 30px;
  border: 2px solid #10ac84;
  background: #1dd1a1;
  padding: 10px 25px 10px 25px;
  color: #fff;
  font-weight: bold;
}

.reminder-container {
  justify-content: center;
  display: flex;
}

.item-wrapper {
  width: 40%;
  margin: 10px;
  position: relative;
}

.reminder-list-item input[type="checkbox"] {
  width: 15px;
  height: 15px;
}

.reminder-list-item {
  color: #fff;
  transition: all 1s;
  background: #273c75;
  width: 100%;
  border-bottom: 2px solid #192a56;
  position: relative;
  padding: 35px 15px 35px 10px;
}

.reminder-list-item:first-of-type {
  border-radius: 20px 20px 0px 0px;
}

.reminder-list-item:last-of-type {
  border-radius: 0px 0px 20px 20px;
}

.reminder-list-item button {
  position: absolute;
  right: 10px;
  all: none;
  background: #ff6b6b;
  border: 1.5px solid #ee5253;
  border-radius: 50px;
  padding: 4px 12px 4px 12px;
  color: #fff;
}

.reminder-list-item:last-of-type {
  border: none;
}

.reminder-list-enter {
  opacity: 0;
  transform: translateX(-300px);
}

.reminder-list-leave-to {
  opacity: 0;
  transform: translateX(300px);
}

.reminder-list-leave-active {
  position: absolute;
}
</style>