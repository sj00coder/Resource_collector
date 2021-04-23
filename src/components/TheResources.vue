<template>
  <base-card>
    <base-button @click="selectTab('stored-resources')" :mode = 'storedResourcestab'>Stored Resources</base-button>
    <base-button @click="selectTab('add-resources')" :mode = 'addResourcestab'> Add Resources</base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResourses.vue';
import AddResources from './AddResource.vue';

export default {
    components:{
        StoredResources,
        AddResources,
    },
    data(){
        return{
            selectedTab:'stored-resources',
             storedResources:[
                {
                    id : 1,
                    title: 'Official-Guide',
                    description: 'The official documentation of vue ',
                    link: 'https://vuejs.org' 
                },
                {
                    id : 2,
                    title: 'Google',
                    description: 'learn how to google.... ',
                    link: 'https://google.org' 
                },
            ],
        };
    },
    computed:{
        storedResourcestab(){
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResourcestab(){
            return this.selectedTab === 'add-resources' ? null : 'flat';
        },
        
    },
    methods:{
        selectTab(tab){
            this.selectedTab = tab;
        },
        deleteResource(resId){
            const res = this.storedResources.findIndex((res) => res.id === resId );
            this.storedResources.splice(res,1);
        }

    },
    provide() {
        return{
            resources:this.storedResources,
            selectTab:this.selectTab,
            deleteResource:this.deleteResource,
        }
    },
    
}
</script>
    BaseButton

<style>

</style>