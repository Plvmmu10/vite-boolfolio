
<template>
  <div class="container mt-5">
    <div class="row row-gap-4">
      <CardComponent v-for="(project, index) in projects" :key="index" :project="project" />

      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item"><button :class="{ 'page-link': true, 'disabled': currentPage === 1 }"
              @click="getProjects(currentPage - 1)">Previous</button></li>
          <li class="page-item" v-for="n in lastPage"><button :class="{ 'page-link': true, 'active': currentPage === n }"
              @click="getProjects(n)">{{ n }}</button>
          </li>

          <li class="page-item"><button :class="{ 'page-link': true, 'disabled': currentPage === 2 }"
              @click="getProjects(currentPage + 1)">Next</button></li>
        </ul>
      </nav>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import CardComponent from './components/CardComponent.vue';
export default {
  name: 'App',
  components: {
    CardComponent
  },
  data() {
    return {
      apiUrl: 'http://127.0.0.1:8000/api',
      projects: [],
      currentPage: 1,
      lastPage: null
    }
  },
  methods: {
    getProjects(numPage) {
      axios.get(`${this.apiUrl}/projects`, {
        params: {
          'page': numPage
        }
      }).then((res) => {
        this.projects = res.data.results.data;
        this.currentPage = res.data.results.current_page;
        this.lastPage = res.data.results.last_page;
      })
    }
  },
  mounted() {
    this.getProjects(1);
  }
}
</script>


<style lang="scss" scoped></style>
