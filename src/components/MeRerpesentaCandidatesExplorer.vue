<template>
  <div class="merepresenta">
    <h2>{{ msg }}</h2>

    <div id='gender_checkboxes'>
      <h3>por genero:</h3>
      <ul class="filtros">
        <li v-for="gender in genderList">
          <input type="checkbox" :id="gender.str_id" :value="gender.str_id" v-model="checkedGenders">
          <label :for="gender.str_id">{{ gender.label }}</label>
        </li>
      </ul>
      <!-- <div class=""> <span>{{genderList}}</span> </div> -->
      <div> <span>{{ checkedGenders }}</span> </div>
    </div>

    <div id='lgtb_checkboxes'>
      <h3>so lgtb:</h3>
      <ul class="filtros">
        <li>
          <input type="checkbox" id="1" value="true" v-model="checkedLgbt">
          <label for="1">sim</label>
        </li>
        <li>
          <input type="checkbox" id="2" value="false" v-model="checkedLgbt">
          <label for="2">nao</label>
        </li>
      </ul>
      <div> <span> {{ checkedLgbt }}</span> </div>
    </div>

    <div id='race_checkboxes'>
      <h3>por raca:</h3>
      <ul class="filtros">
        <li v-for="race in raceList">
          <input type="checkbox" :id="race.str_id" :value="race.str_id" v-model="checkedRaces">
          <label :for="race.str_id">{{ race.label }}</label>
        </li>
      </ul>
      <!-- <div class="">  <span>{{genderList}}</span> </div> -->
      <div> <span>{{ checkedRaces }}</span> </div>
    </div>

    <h2>Seus candidatos sao:</h2>
    <ul class="results">
      <template v-if="checkedGenders.length == 0 && checkedRaces.length == 0 && checkedLgbt.length == 0">
        <li v-for="item in sortedList">
          name: {{ item.name }}, gender: {{ item.gender }}, lgtb: {{ item.lgbt }}, raca: {{ item.race }}, nota: {{ item.nota }}
        </li>
      </template>
      <template v-else>
        <!-- <span> g: {{ checkedGenders.indexOf(item.gender) }} </span> -->
        <li v-for="item in sortedList" v-if="checkedGenders.indexOf(item.gender) !== -1 && checkedRaces.indexOf(item.race) !== -1 && checkedLgbt.indexOf(item.lgbt) !== -1">
          name: {{ item.name }}, gender: {{ item.gender }}, lgtb: {{ item.lgbt }}, raca: {{ item.race }}, nota: {{ item.nota }}
        </li>
      </template>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'MeRerpesentaCandidatesExplorer',
  data () {
    return {
      msg: 'Filtre seus canditatos aqui:',
      //candidateList: [{'id': 1, 'name':'Jordi', 'gender':'Femenino' }, {'id': 2, 'name':'Feli', 'gender':'Masculino' }],
      testList: [{"partido": "AVANTE", "numero": "70456", "lgbt": "false", "id": "aava-santiago", "name": "AAVA SANTIAGO", "gender": "F", "coaligacao": "AVANTE / PR / PV", "lgbt_desc": [], "race": "BRANCA", "nota": 0.9958389632624243, "candidatura_coletiva": "false"}, {"partido": "MDB", "numero": "15999", "lgbt": "false", "id": "abacate", "name": "ABACATE", "gender": "M", "coaligacao": "MDB / SOLIDARIEDADE / PR / PTB / PHS / PSD / PMB / PRP", "lgbt_desc": [], "race": "PARDA", "nota": 0.4231541586464227, "candidatura_coletiva": "false"}, {"partido": "REDE", "numero": "18999", "lgbt": "true", "id": "abadia-santarem", "name": "ABADIA SANTAREM ", "gender": "F", "coaligacao": "PC do B / REDE", "lgbt_desc": [], "race": "PRETA", "nota": 6.031028151919035, "candidatura_coletiva": "false"}, {"partido": "AVANTE", "numero": "70115", "lgbt": "false", "id": "abaete-agora", "name": "ABAETE AGORA", "gender": "M", "coaligacao": "AVANTE", "lgbt_desc": [], "race": "BRANCA", "nota": 6.43420344674113, "candidatura_coletiva": "false"}, {"partido": "PODE", "numero": "19000", "lgbt": "true", "id": "abdala", "name": "ABDALA", "gender": "M", "coaligacao": "PT / PODE", "lgbt_desc": [], "race": "PARDA", "nota": 6.7402676355258615, "candidatura_coletiva": "false"}, {"partido": "PR", "numero": "22444", "lgbt": "false", "id": "abdalla", "name": "ABDALLA", "gender": "M", "coaligacao": "PR / PHS", "lgbt_desc": [], "race": "PRETA", "nota": 1.261823857582559, "candidatura_coletiva": "false"}, {"partido": "PSL", "numero": "17789", "lgbt": "false", "id": "abdias", "name": "ABDIAS", "gender": "M", "coaligacao": "PSL / PATRI / PSC", "lgbt_desc": [], "race": "PARDA", "nota": 8.548107542331488, "candidatura_coletiva": "false"}, {"partido": "DC", "numero": "2766", "lgbt": "false", "id": "abdias-oliveira", "name": "ABDIAS OLIVEIRA", "gender": "M", "coaligacao": "DC", "lgbt_desc": [], "race": "PRETA", "nota": 2.213369673390689, "candidatura_coletiva": "false"}, {"partido": "PSL", "numero": "17123", "lgbt": "true", "id": "abdul-sebba", "name": "ABDUL SEBBA", "gender": "M", "coaligacao": "PSL", "lgbt_desc": [], "race": "BRANCA", "nota": 3.4064392149178078, "candidatura_coletiva": "false"}, {"partido": "PT", "numero": "1306", "lgbt": "false", "id": "abel-alves", "name": "ABEL ALVES", "gender": "M", "coaligacao": "PT", "lgbt_desc": [], "race": "BRANCA", "nota": 9.68782335694462, "candidatura_coletiva": "false"}],
      //genderList: [{'id': 1, 'str_id':'femenino', 'label':'Femenino' },{'id': 2, 'str_id':'masculino', 'label':'Masculino' },{'id': 3, 'str_id':'outro', 'label':'Outro' }],
      genderList: [{'id': 'F', 'str_id':'F', 'label':'Feminino' }, {'id': 'M', 'str_id':'M', 'label':'Masculino' }, {'id': 'outro', 'str_id':'outro', 'label':'Outro gênero' }],
      raceList:[{'id': 'BRANCA', 'str_id':'BRANCA', 'label':'Branca' }, {'id': 'PRETA', 'str_id':'PRETA', 'label':'Preta' }, {'id': 'PARDA', 'str_id':'PARDA', 'label':'Parda' }],
      checkedGenders: [],
      checkedLgbt: [],
      checkedRaces: [],
    }
  },
  computed: {
    sortedList: function() {
      function compare(a, b) {
        if (a.nota > b.nota)
          return -1;
        if (a.nota < b.nota)
          return 1;
        return 0;
      }

      return this.testList.sort(compare);
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

#gender_checkboxes {
  display: inline-block;
}

#race_checkboxes {
  display: inline-block;
}

#lgtb_checkboxes {
  display: inline-block;
}
</style>
