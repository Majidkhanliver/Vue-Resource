<template>
        <base-card>
                <div>

                        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored
                                Resources</base-button>
                        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add New</base-button>
                </div>
        </base-card>
        <component :is="selectedTab"> </component>
</template>
<script>
import AddResource from './AddResource.vue'
import StoredResources from './StoredResources.vue'

export default {
        components: {
                AddResource,
                StoredResources
        },
          data() {
                return {
                        selectedTab: 'stored-resources',
                        storedResource: [
                                {
                                        id: 'official-guide',
                                        title: 'Official Guide',
                                        description: 'The official Vue js Documentation',
                                        link: 'https://vuejs.org'
                                },
                                {
                                        id: 'Google',
                                        title: 'Google',
                                        description: 'The Learning Resource',
                                        link: 'https://google.com'
                                }
                        ],
                }
        },
        provide() {
                return {
                       storedResources:this.storedResource,
                        addResources: this.addResources,
                        removeResource:this.removeResource
                }
                
        },
        computed: {
                storedResButtonMode() {
                        return this.selectedTab === 'stored-resources'? null :'flat'
                },
                addResButtonMode() {
                return this.selectedTab === 'add-resource' ? null :'flat'
               }
        },
      
        methods: {
                setSelectedTab(tab) {
                        this.selectedTab = tab;
                },
                addResources(title, description, link) {
                        const newResource = {
                                id: new Date().toISOString(),
                                title,
                                description,
                                link

                        }
                        this.storedResource.unshift(newResource)
                },
                removeResource(id) {
                        const deleteIndex = this.storedResource.findIndex(res => res.id === id)
                        console.log("Called :",deleteIndex)
                         this.storedResource.splice(deleteIndex,1)
                }
        }
}
</script>
<style scoped>

</style>