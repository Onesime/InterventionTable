<template>
    <tr>
        <td>{{ row.id}}</td>
        <EditRow
            name="first_name"
            :value="row.first_name"
            :row="row"
            :onSubmit="onSubmit"></EditRow>
        <EditRow
                name="last_name"
                :value="row.last_name"
                :row="row"
                :onSubmit="onSubmit"></EditRow>
        <EditRow
                name="email"
                :value="row.email"
                :row="row"
                :onSubmit="onSubmit"></EditRow>
        <EditRow
                name="title"
                :value="row.title"
                :row="row"
                :onSubmit="onSubmit"></EditRow>
        <EditRow
                name="place"
                :value="row.place"
                :row="row"
                :onSubmit="onSubmit"></EditRow>
        <td></td>
    </tr>
</template>

<script>

import EditRow from './EditRow.vue'

export default {
    name: 'Row',
    props: [
        'row'
    ],
    methods: {
        onSubmit: function(name, value, row) {
            row[name] = value;
        }
    },
    components: {
        EditRow: EditRow
    }
}

</script>
