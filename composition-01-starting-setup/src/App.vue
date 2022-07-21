<template>
  <section class="container">
    <user-data :first-name="firstName" :last-name="lastName" class="test"></user-data>  <!-- :age="age" izbačeno radi demonstracije provide-inject -->
    <button @click="setAge">Change Age</button>
    <div>
      <input type="text" placeholder="First Name" v-model="firstName" />
      <input type="text" placeholder="Last Name" ref="lastNameInput" />
      <button @click="setLastName">Set Last Name</button>
    </div>
  </section>
</template>

<script>
import { ref, reactive, computed, watch, provide } from 'vue';
import UserData from './components/UserData.vue';

export default {
  components: {
    UserData
  },
  
  setup() {
    // const uName = ref('Pero');
    const uAge = ref(31);
    const firstName = ref('');
    const lastName = ref('');
    const lastNameInput = ref(null);
    const user = reactive({
      //reactive works only with objects // ref with all kinds of values
      name: 'Pero',
      age: 31,
    });
    console.log(user);
    
    provide('userAge', uAge);

    const uName = computed(function () {
      //computed refs are read only
      return firstName.value + ' ' + lastName.value;
    });
    
    watch([uAge, uName], function (newValues, oldValues) {   //array of values
      console.log('Old age: ' + oldValues[0]);
      console.log('New age: ' + newValues[0]);
      console.log('Old name: ' + oldValues[1]);
      console.log('New name: ' + newValues[1]);
    });

    function setNewAge() {
      // user.age = 45;
      uAge.value = 465;
    }
    function setFirstName(event) {
      firstName.value = event.target.value;
    }    
    function setLastName() {
      lastName.value = lastNameInput.value.value;    //.value of ref from setup f. and value of value (.value.value) is POINTER to input element object
    }

    return {
      userName: uName,
      age: uAge,
      setAge: setNewAge,
      setFirstName,
      firstName,
      lastName,
      lastNameInput,
      setLastName
    };
  },
  // data() {
  //   return {
  //     userName: 'Perica',
  //     age: 45
  //   }
  // },
  // methods: {
  //   setNewAge() {
  //     this.age = 46;
  //   }
  // },
  // watch : {
  //   age(val) {
  //     console.log(val);
  //   }
  // },
  // provide() {
  //   return { age: this.age };
  // }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}

.test {
  margin: 2rem auto;
  background-color: blueviolet;
  width: fit-content;
  padding: 1rem 2rem;
  border-radius: 1rem;
}
</style>
