<template>
  <div id="app">
    <img src="./assets/logo.png">
    
    <h1>{{ msg }}</h1>
    <p>
      <ui-checkbox-group
        vertical
        :options="todoList"
        v-model="checkedNames"
      >
      </ui-checkbox-group>
    </p>

    <ui-alert @dismiss="alertDone = false" type="success" v-show="alertDone">
      We are all Done! Nice work!!!!!!!
    </ui-alert>

    <h1>{{ msg2 }}</h1>
    <p>
      <ui-radio-group
        name="YesOrNo"
        vertical
        :options="yesOrNo.yesOrNoGroup"
        v-model="picked"
      >
      </ui-radio-group>
    </p>

    <div v-if="shallWeGoOn">
      <h1>{{ msg3 }}</h1>

      <ui-textbox label="" placeholder="Add todo" @keydown-enter="addTodoList()" v-model="enteredToDo"></ui-textbox>

      <p>        
        <ui-checkbox-group
        vertical
        :options="dynamicTodoList"
        v-model="checkedDynamicTodoList"
        >
        </ui-checkbox-group>
      </p>

      <ui-alert @dismiss="alertDoneDynamic = false" type="success" v-show="alertDoneDynamic">
        Great work! We are done again!!!!!!!!
      </ui-alert>

    </div>
  </div>
</template>

<script>

const yesOrNoGroup = [
    {
        label: 'Yes Please!',
        value: 'Yes'
    },
    {
        label: 'No Thanks!',
        value: 'No'
    }
];

export default {
  name: 'app',
  data: function () {
    return {
      msg: 'Hackathon Todos',
      todoList: ['Get coffee', 'Gather the guys', 'Review agenda', 'Install nvm, vue-cli, node', 'Play', 'Win!', 'Win!'],
      checkedNames: [],
      alertDone: false,
      msg2: 'Shall We Do More?',
      yesOrNo: {yesOrNoGroup},
      picked: '',
      msg3: 'What do you want to do?',
      enteredToDo: '',
      dynamicTodoList: [],
      checkedDynamicTodoList: [],
      dynamicTodoListCount: 0,
      alertDoneDynamic: false
    }
  },
  watch: {
    checkedNames: {
      handler: function () {
        console.log(this.$data.checkedNames);
        this.$data.result = (this.$data.checkedNames.length === this.$data.todoList.length) ? this.$data.alertDone = true : this.$data.alertDone = false;
      }
    },
    checkedDynamicTodoList: {
      handler: function () {
        console.log(this.$data.checkedDynamicTodoList);
        this.$data.result = (this.$data.checkedDynamicTodoList.length === this.$data.dynamicTodoListCount) ? this.$data.alertDoneDynamic = true : this.$data.alertDoneDynamic = false;
      }
    }
  },
  computed: {
    shallWeGoOn: function () {     
      return this.$data.picked === 'Yes';
    }
  },
  methods: {
    addTodoList: function () {
      this.$data.dynamicTodoList.push(this.$data.enteredToDo);
      this.$data.dynamicTodoListCount += 1;
      this.$data.alertDoneDynamic = false;
      this.enteredToDo = '';
    }
  }
}
</script>

<style>
*,
*::before,
*::after {
    box-sizing: border-box;
}

html {
    font-size: 100%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
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

p {
  margin-left: 500px;
}
</style>
