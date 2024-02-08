<script>
export default {
  name: 'MainPage',
  data() {
    return {
      users: [],
      showModal: true,
      newName: '',
      newPhone: '',
      newOwner: '',
      error: { status: false, message: 'Заполните все поля' },
    };
  },
  mounted() {
    if (this.showModal === true) {
      const usersData = this.getUsers();
      if (usersData.length > 0) {
        this.users = usersData;
      } else {
        this.users = [];
      }
    }
  },

  methods: {
    getUsers() {
      return JSON.parse(localStorage.getItem('users'));
    },
    openModal() {
      this.showModal = false;
    },
    closeModal() {
      this.showModal = true;
    },
    sortByName() {
      this.users = this.getUsers().sort((a, b) => (a.name > b.name ? 1 : -1));
    },
    formSubmit() {
      let prevData = JSON.parse(localStorage.getItem('users'));
      if (this.newName === '' && this.newPhone === '' && this.newOwner === '') {
        this.error.status = true;
      } else {
        if (prevData === null) {
          prevData = [];
        }
        prevData.push({
          name: this.newName,
          phone: this.newPhone,
          owner: this.newOwner,
        });
        localStorage.setItem('users', JSON.stringify(prevData));
        this.newName = '';
        this.newPhone = '';
        this.newOwner = '';
        this.users = this.getUsers();
      }
    },
  },
};
</script>

<template>
  <main>
    <div class="list" v-if="this.showModal">
      <button type="submit" class="openBtn" @click="openModal">Добавить</button>
      <table>
        <tr>
          <th @click="sortByName" class="name">Имя</th>
          <th>Телефон</th>
        </tr>
        <tr v-for="(user, index) in users" :key="(user, index)">
          <td v-if="user.owner === 'да'">+ {{ user.name }}</td>
          <td v-else>{{ user.name }}</td>
          <td>{{ user.phone }}</td>
        </tr>
      </table>
    </div>
    <div class="modal" v-else>
      <div class="info">
        <h3>Добавление пользователя</h3>
        <button type="button" class="closeBtn" @click="closeModal">X</button>
      </div>
      <div v-if="error.status">{{ error.message }}</div>
      <form class="form" v-on:submit.prevent="formSubmit">
        <label>
          Имя
          <input v-model="newName" type="text" />
        </label>
        <label>
          Телефон
          <input v-model="newPhone" type="text" />
        </label>
        <label>
          Начальник
          <select v-model="newOwner">
            <option value="да">Да</option>
            <option value="нет">Нет</option>
          </select>
        </label>
        <button type="submit" class="addBtn" @click="getUsers">
          Сохранить
        </button>
      </form>
    </div>
  </main>
</template>

<style scoped>
/* Main style*/
main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 90vh;
}
/* List style*/
.list {
  width: 50%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

table {
  border: 1px solid;
  width: 60%;
  height: 60%;
}
th,
td {
  border-right: 1px solid;
  border-bottom: 1px solid;
  text-align: center;
  height: 25px;
}
.name {
  cursor: pointer;
}
/* Modal style*/
.modal {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  border: 1px solid;
  height: 50%;
  width: 40%;
  padding: 20px;
}

select,
input {
  width: 200px;
}
.info {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: flex-end;
}

label {
  margin-bottom: 15px;
}
/* Buttons style*/
.openBtn {
  margin-bottom: 20px;
  margin-left: 40%;
  border: 1px solid;
  border-radius: 10px;
  height: 30px;
  width: 100px;
}
h3 {
  margin: 0px;
}
.closeBtn {
  border: 1px solid;
  border-radius: 10px;
}
</style>
