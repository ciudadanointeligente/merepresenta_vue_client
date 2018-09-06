<template>
  <div class="hello">
    <h1>MeRerpesentaCandidatesExplorer</h1>
    <h2>{{ msg }}</h2>
    <div id='gender_checkboxes'>
      <ul class="filtros">
        <li v-for="gender in genderList">
          <input type="checkbox" :id="gender.str_id" :value="gender.label" v-model="checkedGenders">
          <label :for="gender.str_id">{{ gender.label }}</label>
        </li>
      </ul>
      <span>Checked genders: {{ checkedGenders }}</span>
    </div>
    <ul class="results">
      <li v-for="item in candidateList">
        <div v-if="checkedGenders.indexOf(item.gender) !== -1">
          name: {{ item.name }}, gender: {{ item.gender }}<br>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'MeRerpesentaCandidatesExplorer',
  data () {
    return {
      msg: 'Filtre seus canditatos aqui',
      candidateList: [{'id': 1, 'name':'Jordi', 'gender':'Femenino' }, {'id': 2, 'name':'Feli', 'gender':'Masculino' }],
      genderList: [{'id': 1, 'str_id':'femenino', 'label':'Femenino' },{'id': 2, 'str_id':'masculino', 'label':'Masculino' },{'id': 3, 'str_id':'outro', 'label':'Outro' }],
      checkedGenders: []
    }
  },
  computed: {
    filteredCandidatesByGender: function(key) {
      let candidateList = this.candidateList
      return candidateList.map(function(object, index) {
          if(object.str_id == key) {
              return object[key]
          }
      })
      //return "aaaaaaa"
    },
    reversedMessage: function () {
      // `this` points to the vm instance
      return this.msg.split('').reverse().join('')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  //display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
