<template>
  <div class="project">
      <div class="actions">
          <h3 @click="this.showDetails = !this.showDetails">{{  project.title}}</h3>
          <div class="icons">
              <span class="material-icons">edit</span>
              <span @click="deleteProject" class="material-icons">delete</span>
              <span class="material-icons">done</span>
          </div>
      </div>
      <div class="details" v-if="showDetails">
          <p>{{ project.details }}</p>
      </div>
  </div>
</template>

<script>
export default {
    name: "SingleProject",
    props: [ 'project' ],
    data(){
        return {
            showDetails: false,
            uri: "http://localhost:3000/projects/" + this.project.id,
        }
    },
    methods: {
        deleteProject(){
            fetch(this.uri, { method: 'DELETE' })
                .then(() => {
                    this.$emit('delete', this.project.id)
                })
                .catch(err => console.log(err))
        }
    }
}
</script>

<style lang="scss" scoped>
  .project {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
    border-left: 4px solid #e90074;
    .actions {
        display: flex;
        justify-content: space-between;
        align-items: center;

        h3 {
            cursor: pointer;
        }

        .material-icons {
            font-size: 24px;
            margin-left: 10px;
            color: #bbb;
            cursor: pointer;

            &:hover {
                color: #777;
            }
        }
    }
  }
</style>