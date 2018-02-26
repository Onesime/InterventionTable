<template>
    <td>
        <div v-show="!isEditing" v-on:dblclick="onDblClick()"><label>{{ value }}</label></div>
        <input v-show="isEditing"
               v-model="value"
               v-on:focusout="isDone()"
               v-on:keyup.enter="isDone()"
               v-on:keyup.esc="isDone()"
               :ref="'input'">
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
        onDblClick: function(event) {
            this.isEditing = true;
            setTimeout(() => {
                this.$refs['input'].focus()
            }, 0)
        },
        isDone: function() {
            this.isEditing = false;
            this.onSubmit(this.name, this.value, this.row);
        }
    }
}

</script>