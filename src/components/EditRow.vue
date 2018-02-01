<template>
    <td>
        <div v-show="!isEditing" v-on:dblclick="onDblClick()"><label>{{ value }}</label></div>
        <input v-show="isEditing"
               v-model="value"
               v-on:focusout="isDone()"
               v-on:keyup.enter="isDone()"
               v-on:keyup.esc="isDone()">
    </td>
</template>

<script>

export default {
    name: 'EditRow',
    props: [
        'name', 'value', 'row', 'onSubmit'
    ],
    data: function() {
        return {
            isEditing: false
        }
    },
    methods: {
        onDblClick: function() {
            this.isEditing = true;
        },
        isDone: function() {
            this.isEditing = false;
            this.onSubmit(this.name, this.value, this.row);
        }
    }
}

</script>