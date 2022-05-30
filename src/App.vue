<template>
  <div class="home__container">
    <Header title="Reminders" @toggle-addReminder="toggleAddReminder" />
    <!-- toggle add reminder modal visbility conditonally  -->
    <div v-if="showAddReminder">
      <AddReminder
        @add-reminder="addReminder"
        @toggle-addReminder="toggleAddReminder"
      />
    </div>
    <!-- passing the reminders array to the reminders component -->
    <!-- recieves the custom event from reminders component -->
    <Reminders
      @delete-reminder="deleteReminder"
      @toggle-alert="toggleAlert"
      :reminders="reminders"
    />
    <Footer :reminders="reminders" />
  </div>
</template>

<script>
// importing components
import Header from "./components/Header.vue";
import Reminders from "./components/Reminders.vue";
import Footer from "./components/Footer.vue";
import AddReminder from "./components/AddReminder.vue";

export default {
  name: "App",
  components: { Header, Reminders, Footer, AddReminder },
  data() {
    return {
      reminders: [], // Array to store reminders
      showAddReminder: false, // toggle modal
    };
  },
  methods: {
    async addReminder(reminder) {
      // add reminder to db.json
      const response = await fetch("http://localhost:5000/reminders", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(reminder),
      });

      const data = await response.json();

      // pushes the response into the reminders array
      this.reminders.push(data);
    },
    async deleteReminder(id) {
      // delete reminder in db.json
      const response = await fetch(`http://localhost:5000/reminders/${id}`, {
        method: "DELETE",
      });

      if (response.status === 200) {
        // filters the reminders array and reassigns it after removing the selected reminder
        this.reminders = this.reminders.filter(
          (reminder) => reminder.id !== id
        );
      } else {
        alert("Erorr deleting reminder");
      }
    },
    async toggleAlert(id) {
      // fetch the reminder to update alert status
      const reminderToToggle = await this.fetchReminder(id);
      // reverses the alert status on the reminder object
      const reminderUpdated = {
        ...reminderToToggle,
        alert: !reminderToToggle.alert,
      };

      const response = await fetch(`http://localhost:5000/reminders/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(reminderUpdated),
      });

      const data = await response.json();

      // returns an updated reminders array by changing the status according to fetch response
      this.reminders = this.reminders.map((reminder) =>
        reminder.id === id ? { ...reminder, alert: data.alert } : reminder
      );
    },
    toggleAddReminder() {
      // reverses value of showAddReminder
      this.showAddReminder = !this.showAddReminder;
    },

    async fetchReminders() {
      // fetch all reminders
      const response = await fetch("http://localhost:5000/reminders");
      const data = await response.json();
      return data;
    },
    async fetchReminder(id) {
      // fetch a single reminders
      const response = await fetch(`http://localhost:5000/reminders/${id}`);
      const data = await response.json();
      return data;
    },
  },
  created: function () {
    // fetch reminders from db.json
    fetch("http://localhost:5000/reminders")
      .then((response) => response.json().then((data) => data))
      .then((result) => (this.reminders = result))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Quicksand&display=swap");

* {
  margin: 0;
  padding: 0;
  font-family: "Quicksand", sans-serif;
  list-style: none;
  text-decoration: none;
}

:root {
  --bg-color: #222327;
  --primary-color: #00e0bb;
  --secondary-color: #ff4545;
  --primary-hover: #00e0bb18;
}

#app {
  width: 100%;
  height: 100vh;
  background-color: var(--bg-color);
  display: flex;
  justify-content: center;
  align-items: center;
}

.home__container {
  width: 30rem;
  padding: 2rem;
  border-radius: 15px;
  background: #fff;
}

.home__container .list {
  margin-top: 18px;
}

.home__container .list li:not(:last-child) {
  margin-bottom: 15px;
}

.home__container .list li .content {
  padding: 10px 10px;
  border-radius: 6px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}

.priority {
  border-left: 5px solid var(--secondary-color);
}

.normal {
  border-left: 5px solid var(--primary-color);
}

.home__container .list li:hover .content {
  background: var(--primary-hover);
}

.home__container .list li .content h1 {
  color: #666;
  font-size: 18px;
  font-weight: 700;
  line-height: 20px;
}

.home__container .list li .content p {
  color: #aaa;
  line-height: 15px;
  font-size: 15px;
}

.home__container .list li .content i {
  cursor: pointer;
  color: #fff;
  padding: 8px;
  font-size: 1.2rem;
  border-radius: 5px;
  background-color: var(--secondary-color);
  transition: all 0.3s;
}
</style>
