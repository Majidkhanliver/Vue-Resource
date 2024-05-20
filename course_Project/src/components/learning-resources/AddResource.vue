<template>
        <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
                <template #default>
                        <p>Unfortunately, at least one input value is invalid</p>
                        <p>Please check all input and make sure at least a few characters into each input field.</p>
                </template>
                <template #actions>
                        <base-button @Click="confirmError">Okay</base-button>
                </template>
         </base-dialog>
        <base-card>
                <form @submit.prevent="addResource()">
                        <div class="form-control">

                                <label for="">Title</label>
                                <input type="text" name="title" id="title" ref="titleInput">
                        </div>


                        <div class="form-control">

                                <label for="description">Title</label>
                                <textarea rows="3" type="text" name="description" id="description"
                                        ref="descriptionInput" />
                        </div>

                        <div class="form-control">

                                <label for="link">link</label>
                                <input type="url" name="link" id="link" ref="linkInput">
                        </div>
                        <base-button type="submit">Submit</base-button>
                </form>
        </base-card>
</template>
<script>
export default {
        inject: ['addResources'],
        data() {
                return {
                        inputIsInvalid:false,
                }
       },
        methods: {
                addResource()
                {
                        let name = this.$refs.titleInput.value;
                        let description = this.$refs.descriptionInput.value;
                        let link = this.$refs.linkInput.value;
                        if (name.trim() == '' || description.trim() === '' || link.trim() === '')
                        {
                                this.inputIsInvalid = true;
                                        return
                        }
                        this.addResources(name,description,link)
                },
                confirmError() {
                        this.inputIsInvalid = false;
                }
        }
}
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