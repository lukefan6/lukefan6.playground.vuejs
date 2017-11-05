<template>
  <div class="hello">
    <b-container class="bv-example-row">
      <b-row>
        <b-col offset-lg="2" lg="8">
          <b-input-group>
            <b-form-input v-model="daysToAdd" type="number"></b-form-input>
            <b-input-group-button slot="right">
              <b-button variant="success" v-on:click="runAgain">
                Run
              </b-button>
            </b-input-group-button>
          </b-input-group>
        </b-col>
      </b-row>
      <b-row>
        <b-col offset-lg="2" lg="8">
          <hr>
        </b-col>
      </b-row>
      <b-row>
        <b-col offset-lg="2" lg="8">
          <b-alert variant="info" dismissible :show="showDismissibleAlert" @dismissed="showDismissibleAlert=false">
            <h1>{{ msg }}</h1>
          </b-alert>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import * as moment from 'moment';

function getNextRandomNumber(start, end) {
  const base = Math.random() * end;
  return Math.floor(base + start);
}

function getNextRandomDate(baseline, daysToAdd) {
  const nextAddedHours = getNextRandomNumber(0, daysToAdd * 24);

  return moment(baseline).add(nextAddedHours, 'hours');
}

export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: '',
      daysToAdd: 7,
      showDismissibleAlert: false,
    };
  },
  // define methods under the `methods` object
  methods: {
    runAgain() {
      const date = getNextRandomDate(new Date(), this.daysToAdd);
      this.msg = moment(date).format('YYYY-MM-DD HH:00');
      this.showDismissibleAlert = true;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* h1,
h2 {
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
} */
</style>
