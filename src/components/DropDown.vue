<template v-slot="option"  slot-scope="props">

  <h3>SEARCHABLE DROPDOWN</h3>
  <section class="dropdown-wrapper">
    <div @click="isVisibleUser = !isVisibleUser" class="selected-item">
      <span v-if="selectedItem" class="selected-text" >
       
         {{`${selectedItem.name},${selectedItem.username},${selectedItem.email}
        `}}
         
  
      </span>
      <span v-else class="selected-text">Поиск по имени</span>
      <svg
        :class="isVisibleUser ? 'dropdown' : ''"
        class="dropdown-icon"
        width="13"
        height="7"
        viewBox="0 0 13 7"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M7.10793 6.76714C6.78181 7.07762 6.25307 7.07762 5.92696 6.76714L0.244587 1.35721C-0.0815288 1.04673 -0.0815289 0.543341 0.244586 0.232861C0.570703 -0.07762 1.09944 -0.0776205 1.42556 0.23286L6.50041 5.0644L11.5744 0.233644C11.9006 -0.0768371 12.4293 -0.0768371 12.7554 0.233644C13.0815 0.544124 13.0815 1.04751 12.7554 1.35799L7.23227 6.61633C7.1981 6.67005 7.15666 6.72075 7.10793 6.76714Z"
          fill="#898989"
        />
      </svg>
    </div>
    <div v-if="isVisibleUser" class="dropdown-popover">
      <input  v-model="searchUser" type="text" placeholder="Поиск"/>
      <p v-if="filteredUser.length === 0">Пользователь не найден</p>
      <div class="options">
        <ul  >
          <li @click="selectItem(user)"
            v-for="(user, index) in filteredUser"
            :key="`user-${index}`"
          >
           <input type="checkbox" id='1' >
           <label for="1">
             {{user.name}}
          </label>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      searchUser: '',
      selectedItem: null,
      isVisibleUser: false,
      userArray: [],
    };
  },
  computed: {
    filteredUser() {
      const users = this.searchUser.toLowerCase();
      if (this.searchUser === '') {
        return this.userArray;
      }
      return this.userArray.filter((user) => {
        return Object.values(user).some((word) =>
          String(word).toLowerCase().includes(users)
        );
      });
    },
  },
  methods: {
    selectItem(user) {
      this.selectedItem = user;
      
    },
  highlight(text){
    if(!this.query) return text;
    let regEx = new RegExp(this.query,'i');
    let index = text.search(regEx)
    let replaceText = text.substring(index,index + this.query.length);
    return text.replace(regEx, `<span class="autoComplete_highlighted">${replaceText}</span>`);}
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((json) => {
        console.log(json);
        this.userArray = json;
      });
  },
};
</script>

<style>
h3 {
  margin-top: 67px;
  padding-left: 25px;
}
section {
  padding-left: 25px;
}

.dropdown-wrapper {
  position: relative;
}

.selected-item {
  display: flex;
  justify-content: space-between;
  width: 300px;
  border: 1px solid #0e1319;
  border-radius: 5px;
  padding: 10px 10px 9px 10px;
  align-items: center;
  color: #888888;
}
.selected-text {
  font-weight: 400;
  font-size: 13px;
  line-height: 15px;
  letter-spacing: 1.5px;
}

.dropdown-popover {
  position: absolute;
  border: 1px solid #0e1319;
  border-radius: 5px;
  top: 45px;
  width: 300px;
}

.dropdown-icon {
  transform: rotate(180deg);
  transition: all 0.4 ease;
}

.dropdown-icon.dropdown {
  transform: rotate(0deg);
}

input {
  margin-left: 8px;
  margin-top: 10px;
  margin-bottom: 11px;
  width: 280px;
  padding-top: 10px;
  padding-left: 10px;
  padding-bottom: 9px;
  border: 1px solid #c4c4c4;
  border-radius: 5px;
}

.options {
  width: 100%;
}

ul {
  list-style: none;
  overflow-y: scroll;
  max-height: 210px;
}
li {
  padding-top: 13px;
  padding-bottom: 12px;
  padding-left: 20px;
}

p {
  text-align: center;
  padding-bottom: 12px;
}

.autoComplete_highlighted{
  color: red;
}
</style>