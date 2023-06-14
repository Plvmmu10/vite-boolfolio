<template>
    <div class="container">
        <div v-if="project" class="bg-dark text-white p-2">
            <h1>{{ project.name }}</h1>

            <p>{{ project.description }}</p>

            <p>Technology: {{ project.technology.name }}</p>

            <div>
                <span class="badge rounded-pill bg-danger mx-1" v-for="tag in project.tags">{{ tag.name }}</span>
            </div>
        </div>

        <div v-else>
            <LoaderApp />
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import LoaderApp from '../components/LoaderApp.vue';
export default {
    name: 'SingleProject',
    components: {
        LoaderApp
    },
    data() {
        return {
            apiUrl: 'http://127.0.0.1:8000/api',
            project: null,
        }
    },
    methods: {
        getProjects() {
            axios.get(`${this.apiUrl}/projects/${this.$route.params.slug}`).then((res) => {
                console.log(res.data.results);
                if (res.data.success) {
                    this.project = res.data.results;
                } else {
                    this.$router.push({ name: 'not-found' })
                }
            })
        }
    },
    mounted() {
        this.getProjects();
    }
}

</script>

<style lang="scss" scoped></style>