<template>
    <form :action="action" method="POST">
        <input type="hidden" name="_method" :value="method" v-if="method !== 'POST'">

        <slot></slot>

        <button type="submit" class="btn btn-primary btn-sm" @click.prevent="search" v-if="type === 'ajax'">{{ btnSearchText }}</button>
        <button type="submit" class="btn btn-primary btn-sm" v-else>{{ btnSearchText }}</button>
    </form>
</template>

<script>
    export default {
        props: {
            // Will use formData's key as query string's name
            formData: {
                type: Object,
                required: true,
            },
            btnSearchText: {
                type: String,
                default: 'Search'
            },
            // Only for traditional form
            action: {
                type: String,
                default: '',
            },
            // Only for traditional form
            method: {
                type: String,
                default: 'POST',
                validator: function (value) {
                    // The value must match one of these strings
                    return ['POST', 'DELETE', 'OPTION', 'PATCH', 'PUT'].indexOf(value) !== -1
                },
            },
            type: {
                validator: function (value) {
                    // The value must match one of these strings
                    return ['traditional', 'ajax'].indexOf(value) !== -1
                },
                default: 'traditional'
            }
        },
        methods: {
            search() {
                var queryString = Object.keys(this.formData).map(key => key + '=' + this.formData[key]).join('&');
                this.$emit('remote-call', queryString)
            }
        }
    }
</script>
