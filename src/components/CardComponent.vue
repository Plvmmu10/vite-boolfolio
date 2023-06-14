<template>
    <div class="col-4">
        <div class="card bg-dark text-white">
            <div class="card-image">
                <img :src="project.image" :alt="project.name">
            </div>

            <div class="card-body">
                <h4>{{ project.name }}</h4>

                <p class="fst-italic">{{ project.description }}</p>

                <p>Technology: {{ project.technology.name }}</p>

                <p>Tags:
                    <span v-for="(tag, index) in project.tags" class="badge rounded-pill text-bg-danger text-white">
                        <span v-if="tag.name.trim().length !== 0">{{ tag.name }}</span>
                        <span v-else>Nessun tag</span>
                    </span>
                </p>


                <router-link :to="{ name: 'single-project', params: { slug: project.slug } }" class="btn btn-primary"><i
                        class="fa-solid fa-eye"></i></router-link>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardComponent',
    props: ['project']
}
</script>

<style lang="scss" scoped></style>