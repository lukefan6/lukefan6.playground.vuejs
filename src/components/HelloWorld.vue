<template>
  <div class="hello">
    <b-container class="bv-example-row">
      <b-row>
        <b-col offset-lg="2" lg="8">
          <b-form>
            <b-form-group label="Random Date">
              <b-input-group>
                <b-form-input v-model="daysToAdd" @keyup.enter.native="runAgain" type="number"></b-form-input>
                <b-input-group-button slot="right">
                  <b-button variant="success " v-on:click="runAgain">
                    Run
                  </b-button>
                </b-input-group-button>
              </b-input-group>
              <hr>
              <b-alert variant="info " dismissible :show="showDismissibleAlert " @dismissed="showDismissibleAlert=false ">
                <h2>{{ msg }}</h2>
              </b-alert>
            </b-form-group>
          </b-form>
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
            afterHour: 10,
            beforeHour: 23,
        };
    },
    // define methods under the `methods` object
    methods: {
        runAgain() {
            let shouldRetry = true;
            let date = moment();
            while (shouldRetry) {
                date = getNextRandomDate(new Date(), this.daysToAdd);
                shouldRetry = this.isInRange(date) === false;
            }

            this.msg = moment(date).format('YYYY-MM-DD HH:00');
            this.showDismissibleAlert = true;

            this.$copyText(this.msg);
        },
        isInRange(date) {
            const from = moment(date).hour(this.afterHour);
            const to = moment(date).hour(this.beforeHour);

            return moment(date).isBetween(from, to);
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* .hello {
  padding: 20px;
} */
</style>
