<template>
  <div class="home-view-container">
    <h1>Adopt a new best friend.</h1>
    Cats : {{ getAllCats.length }}
    <br><br>

    Dogs : {{ getAllDogs.length }}
    <br><br>

    All : {{ animalsCount }}
    <br><br>

    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>
    <br><br>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group
        id="input-group-1"
        type="text"
        label="Pet's Name :"
        label-for="input-1"
        >
        <b-form-input
          id="input-1"
          v-model="formData.name"
          placeholder="Enter pet's name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Species :"
        label-for="input-2"
        >
        <b-form-select
          id="input-2"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group
        id="input-group-3"
        label="Pet's Age :"
        label-for="input-3"
        >
        <b-form-input
          id="input-3"
          type="number"
          v-model="formData.age"
          placeholder="Enter pet's age"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats',
      'getAllDogs'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)

      // reset fields
      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}
</script>
