<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" 
        :mode="storedResButtonMode"
        >Stored Resources
        </base-button>
        <base-button @click="setSelectedTab('add-resource')"
        :mode="addResourcesMode">Add Resource</base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>
<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
    export default {
        components: {
            StoredResources,
            AddResource
        },
        data() {
            return {
                selectedTab: 'stored-resources',
                storedResources: [
                    {
                        id: 'official-guide',
                        title: 'Official Guide',
                        description: 'The official Vue Js documentation.',
                        link: 'https://vuejs.org/',
                    },
                    {
                        id: 'google',
                        title: 'Google',
                        description: 'Learn To Google',
                        link: 'https://www.google.com/',
                    },
                ],
            };
        },
        // provide & inject rule (provide a method in this component & injetc that method in another component where it is to be used)
        provide() {
            return {
                resources: this.storedResources,
                addResource: this.addResource,
                removeResources: this.removeResources
            }     
        },
        computed: {
            storedResButtonMode() {
                return this.selectedTab === 'stored-resources' ? null : 'flat';
            },
            addResourcesMode() {
                return this.selectedTab === 'add-resource' ? null : 'flat';
            },
        },
        methods: {
            setSelectedTab(tab) {
                this.selectedTab = tab;
            },
            addResource(title, description, url) {
                const newResource = {
                    id: new Date().toISOString(),
                    title: title,
                    description: description,
                    link: url
                };
                this.storedResources.unshift(newResource);
                this.selectedTab = 'stored-resources';
            },
            removeResources(resId) {
                // how we delete an element in an array using findindex
                const resIndex = this.storedResources.findIndex(res => res.id === resId);
                this.storedResources.splice(resIndex, 1);
            },
        },
    };
</script>