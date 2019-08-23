<template>
  <div id="app">
    <div>
      <label>Name:</label>
      <input type="text" v-model="name">
      <button @click="submitName()">Add</button>
    </div>

    <div>
      <table>
        <thead>
          <tr>
          <th>Name</th>
          <th>Edit</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="people of names" :key="people['.key']">
            <td>{{ people.name }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase'

let firebaseConfig = {
  apiKey: "AIzaSyAZKnbUtIg8t_HtFjuibasfUTevizkqcwI",
  authDomain: "urus-6cccf.firebaseapp.com",
  databaseURL: "https://urus-6cccf.firebaseio.com",
  projectId: "urus-6cccf",
  storageBucket: "",
  messagingSenderId: "687918059990",
  appId: "1:687918059990:web:98498d0a75d23676"
};

let app = Firebase.initializeApp(firebaseConfig)
let db = app.database()

let namesRef = db.ref('names')

export default {
  name: 'app',
  data () {
    return {
      name:'Dheja',
  }
  },
  computed: {
    names() {
      return namesRef
    }
  },
  methods: {
    submitName() {
      namesRef.push({name: this.name, edit: false});
    }
  }
}
</script>

<style>
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
button{
  background-color: transparent;
  border: 2px, solid, black;
}
</style>
