<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
import * as moment from 'moment';

function getNextRandomNumber(start, end) {
  return Math.floor((Math.random() * end) + start);
}

function getNextRandomDate(baseline, daysToAdd) {
  const nextAddedHours = getNextRandomNumber(0, daysToAdd * 24);

  return moment(baseline).add(nextAddedHours, 'hours');
}

export default {
  name: 'HelloWorld',
  data() {
    const date = getNextRandomDate(new Date(), 7);
    return {
      msg: moment(date).format('YYYY-MM-DD HH:00'),
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
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
}
</style>
