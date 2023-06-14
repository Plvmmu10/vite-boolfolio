<template>
    <div v-if="projects == 0">
        <LoaderApp />
    </div>


    <div v-else>
        <div class="container" id="Project-list">
            <h1>{{ title }}</h1>
            <div class="row gy-4 mb-4">
                <CardComponent v-for="(project, index) in projects" :key="project.id" :project="project" />
            </div>
        </div>
        <nav aria-label="Page navigation example">
            <ul class="pagination">
                <li class="page-item"><button :class="{ 'page-link': true, 'disabled': currentPage === 1 }"
                        @click="getProjects(currentPage - 1)">Previous</button></li>
                <li class="page-item" v-for="n in lastPage"><button
                        :class="{ 'page-link': true, 'active': currentPage === n }" @click="getProjects(n)">{{ n }}</button>
                </li>

                <li class="page-item"><button :class="{ 'page-link': true, 'disabled': currentPage === lastPage }"
                        @click="getProjects(currentPage + 1)">Next</button></li>
            </ul>
        </nav>
    </div>
</template>

<script>
import axios from 'axios';
import CardComponent from '../components/CardComponent.vue';
import LoaderApp from '../components/LoaderApp.vue';
export default {
    'name': 'ProjectList',
    components: {
        CardComponent,
        LoaderApp
    },
    data() {
        return {
            apiUrl: 'http://127.0.0.1:8000/api',
            projects: [],
            currentPage: 1,
            lastPage: null,
            title: 'Projects List'
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