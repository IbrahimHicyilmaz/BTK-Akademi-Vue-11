<template>
    <div class="project" :class="{complate: project.complate}">
        <div class="actions">
            <h3 @click="showDetails = !showDetails">{{project.title}}</h3>
            <div class="icons">
                <router-link :to="{name:'EditProject', params:{id:project.id}}"><span class="material-icons">edit</span></router-link>
                <span @click="deleteProject" class="material-icons">delete</span>
                <span @click="toggleComplate" class="material-icons tick">done</span>
            </div>
        </div>
        <div v-if="showDetails" class="details">
            <p>{{project.details}}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ["project"],
    data() {
        return {
            showDetails: false,
            uri: "http://localhost:3000/projects/" + this.project.id,
        };
    },
    methods: {
        deleteProject() {
            fetch(this.uri, { method: "DELETE" })
                .then(() => this.$emit("delete", this.project.id));
        },
        toggleComplate() {
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ complate: !this.project.complate })
            }).then(() => this.$emit("complate", this.project.id)).catch(err => console.log(err));
        }
    },
}
</script>

<style>
.project {
    margin: 20px auto;
    background: #fff;
    padding: 10px 20px;
    border-radius: 5px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
    border-left: 4px solid #ff5500;
}

h3 {
    cursor: pointer;
}

.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}

.material-icons:hover {
    color: #777;
}

.project.complate {
    border-left: 4px solid #76dd78;
}
.project.complate .tick {
    color: #76dd78;
}
</style>