<template>
    <div class="message">
        <div class="message-header">
            Push to the stream...
        </div>

        <div class="message-body">
            <form action="" @submit.prevent="onSubmit" @keydown="form.errors.clear()">
                <p class="controll">
                    <textarea v-model="form.body" class="textarea" placeholder="I have something to say..." cols="30" rows="10"></textarea>
                    <span class="help is-danger" v-if="form.errors.has('body')" v-text="form.errors.get('body')"></span>
                </p>

                <p class="controll">
                    <button class="button is-primary" :disabled="form.errors.any()">Submit</button>
                </p>
            </form>
        </div>
    </div>
</template>

<script>
    export default {

        data() {
            return {
                form: new Form({ body: '' })
            }
        },

        methods: {
            onSubmit() {
                // submit an ajax request to the server
                this.form
                    .post('/statuses')
                    .then(status => this.$emit('completed', status))
                    .catch(response => {
                        console.log(response);
                    });
            }
        }
    }
</script>

<style scoped>

</style>
