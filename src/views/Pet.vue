<template>
  <div>
    <h1>{{ animal.name }} ({{ animalType }})</h1>
    <p>Age: {{ animal.age }} years old</p>
    <p>Breed: {{ animal.breed}}</p>
  </div>
</template> 

<script>
import { mapState } from 'vuex'


export default {
  data() {
    return {
      animal: {},
      animalType: ''
    }
  },

  computed: {
    ...mapState([
      'cats',
      'dogs'
    ])
  },
  mounted(){
      const animal = this[this.$route.params.species][this.$route.params.id]
      this.animal = animal
      this.animalType = this.$route.params.species.slice(0, -1)
    }
  }
</script>