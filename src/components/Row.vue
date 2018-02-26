<template>
    <tr>
      <td class="checkbox"><input class="inputs" type="checkbox" :id="'check' + row.id" ></td>
      <td class="id">{{ row.id}}</td>
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
      <td class="buttons">
          <input type="button" class="btn btn-default" value="X" v-on:click="suppr(index)"/>
          <button v-on:click="selectedRowChanged" type="button" class="btn btn-primary btn-sm" data-toggle="modal" data-target="#myModal">
              <i class="far fa-edit"></i>
          </button>
      </td>
    </tr>
</template>

<script>

import EditRow from './EditRow.vue'

export default {
    name: 'Row',
    props: [
        'row',
        'json',
        'suppr',
        'index',
    ],
    methods: {
        onSubmit: function(name, value, row) {
            row[name] = value;
        },
        selectedRowChanged: function() {
            this.$parent.$emit('selectedRowChanged', { row: this.row })
        }
    },
    components: {
        EditRow: EditRow
    }
}

</script>
