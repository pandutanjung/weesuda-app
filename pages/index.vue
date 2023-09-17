<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom d-flex align-items-center justify-content-between py-2">
        <h5>University Review</h5>
        <div class="d-flex align-items-center">
          <input
          v-model="searchQuery"
          type="text"
          class="form-control"
          placeholder="Search"
          >
          <div class="d-flex align-items-center justify-content-end w-100">
          <span class="me-2">View As</span>
          <button
            class="btn btn-outline-secondary py-1 px-3"
            @click="isGrid = !isGrid">
            {{ isGrid ? 'Grid' : 'List' }}
          </button>
        </div>
        </div>
      </div>
      <div clas="list-university row">
        <!-- <CardItem :university="university[0]" :isGrid="isGrid" />
        <CardItem :university="university[1]" :isGrid="isGrid" />
        <CardItem :university="university[2]" :isGrid="isGrid" /> -->
        <CardItem
        v-for="(university, i) in resultQuery"
        :key="i"
        :university="university"
        :isGrid="isGrid"
        />
      </div>
      <div class="action py-2">
      <a v-if="!isCreating" href="#" class="add-button"  @click="isCreating = !isCreating">Add University</a>
      <div v-else class="add-card" >
      <section class="form">
        <form v-on:submit.prevent="handleSubmit">

        <div class="field">
          <div class="control">

            <div class="card mb-2">
              <div class="card-body d-flex flex-column p-0">
                <input v-model="form.university" class="form-control border-0 mb-2" placeholder="University" type="text" >
                <textarea v-model="form.review" class="form-control border-0 small" placeholder="Review" rows="3"></textarea>
              </div>
            </div>
          </div>
        </div>
          <div class="button-wrapper d-flex">
            <form v-on="handleSubmit">
              <div class="field is-grouped">
                <div class="control">

                  <button class="btn btn-primary me-2">Save</button>
                  <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
                </div>
              </div>
            </form>
          </div>
        </form>
      </section>
      <div>
        <ul>
          <li v-for="item in inputanForm" :key="item">
            {{ form }}
          </li>
        </ul>
      </div>
      </div>
    </div>
  </div>
</div>
</template>
<script>
import CardItem from '~/components/Card/CardItem.vue'
export default {
  components:{
    CardItem
  },
  data(){
    return{
      searchQuery: '',
      isGrid: true,
      isCreating: false,  
      form : {
        university: '',
        review: ''
      },
      inputanForm: []
    }
  },
  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.university.filter((item) => {
          return this.searchQuery
          .toLowerCase()
          .split(" ")
          .every((v) => item.name.toLowerCase().includes(v));
        });
      } else {
        console.log(this.university)
        return this.university
      }
    }
  },
  methods: {
    handleSubmit() {
      const item = {
        form: this.form
      }
      this.inputanForm.push(item)
    }
  }
}
</script>
<style>
</style>