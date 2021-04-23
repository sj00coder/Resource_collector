<template>
<base-dialog v-if="isDataInvalid" title="Invalid Data" @close="okayButton">
    <template #default>
        <p>This data is invalid</p>
        <p>Please enter all data inputs</p>

    </template>
    <template #actions>
        <base-button @click = "okayButton">Okay</base-button>
    </template>
</base-dialog>
<base-card>
  <form @submit.prevent = "onAddbutton" >
    <div class="form-control">
      <label for="title">Name:</label>
      <input type="text" id="title" name="title" v-model="resource.title"/>
    </div>
    <div class="form-control">
      <label for="description">Description:</label>
      <textarea rows="3" id="description" name="description"  v-model="resource.description"/>
    </div>
    <div class="form-control">
      <label for="link">URL:</label>
      <input type="url" id="link" name="link" v-model="resource.link"/>
    </div>
    <base-button type="submit" >Add</base-button>
  </form>
</base-card>
</template>

<script>
export default {
  
    inject:[
        'resources',
        'selectTab'
    ],
    data() {
        return {
            resource: {
                id:this.title,
                title: '',
                description: '',
                link: '',
            },
            isDataInvalid: false,
        };
    },
    methods: {
        onAddbutton(){
            if(this.resource.title.trim() === '' ||this.resource.description.trim() === '' ||this.resource.link.trim() === ''){
                this.isDataInvalid = true;
                return;
            }
            this.resources.push(this.resource);
            this.selectTab('stored-resources');
        },
        okayButton(){
            this.isDataInvalid = false;
        }
    }
 };
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>