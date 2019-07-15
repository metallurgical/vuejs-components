<template>
    <div class="form-group row" v-if="inputType === 'column'">
        <label :for="name" class="col-sm-2 col-form-label">{{ label }}</label>
        <div class="col-sm-10">
            <input :type="type" class="form-control" :id="name" :value="inputValue" :placeholder="placeholder"
                   v-on:input="$emit('input', $event.target.value)">
        </div>
    </div>

    <div class="form-group" v-else>
        <label :for="name">{{ label }}</label>
        <input :type="type" class="form-control" :id="name" :value="inputValue" :placeholder="placeholder"
               v-on:input="$emit('input', $event.target.value)">
    </div>
</template>

<script>
    export default {
        props: {
            inputType: {
                type: String,
                default: 'row',
            },
            type: {
                type: String,
                default: 'text'
            },
            label: {
                type: String,
                required: true
            },
            // Required if sending traditional FORM action
            name: {
                type: String,
            },
            // For input's default value
            inputValue: {
                type: String,
                default: ''
            },
            placeholder: {
                type: String,
                default: ''
            },
            // For simulate v-model
            value: {
                type: String,
            }
        }
    }
</script>
