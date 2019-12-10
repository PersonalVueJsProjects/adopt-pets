<template>
  <div class="home">
    <div>
      <h1>Adopt A new Best Friend</h1>
      {{ animalsCount }}
      <button class="btn btn-primary" @click="togglePetForm">Add New Pet</button>

    <b-form @submit.prevent="onSubmit" v-if="showPetForm">

      <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-group-2">
        <b-form-input
          id="input-2"
          type="number"
          v-model="form.age"
          required
          placeholder="Enter Age"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>

    </b-form>


    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'home',
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm(){
      this.showPetForm = !this.showPetForm
    },
    onSubmit(){
    const { species, age, name } = this.form
    const payload = {
      species,
      pet: {
        name,
        age
      }
    }
    this.addPet(payload)
  this.form = {
        name:'',
        age: 0,
        species: null
    }
  }
  },
  data(){
    return {
      showPetForm: false,
      form: {
        name:'',
        age: 0,
        species: null
      }
    }
  },

  computed: {
    ...mapGetters([
      'animalsCount'
    ])
  }
   
}
</script>
