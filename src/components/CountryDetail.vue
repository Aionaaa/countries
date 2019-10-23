<template lang="html">
  <div v-if="country">
    <h3>{{country.name}}</h3>
    <p>{{country.capital}}</p>
    <p>{{country.population}}</p>
    <img id="flagImg" :src="country.flag">
  </div>
</template>

<script>
export default {
  name: 'country-detail',
  props: ['country']
}
</script>

<style lang="css" scoped>
#flagImg{
  width: 250px;
}
</style>
