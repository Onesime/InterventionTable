<template>
    <th class="thordering" v-on:click="doCallback()">
        <label>{{ name }}
            <span v-show="isOrdered && ordering.isDesc"><i class="fa fa-angle-down"></i></span>
            <span v-show="isOrdered && !ordering.isDesc"><i class="fa fa-angle-up"></i></span>
        </label><br>
        <input v-on:click.stop v-on:keyup="search()" v-model="value">
    </th>
</template>

<script>

    export default {
        name: 'THOrdering',
        props: [
            'field',
            'name',
            'ordering',
        ],
        data() {
            return {
                isDown: false,
                value: ''
            }
        },
        computed: {
            isOrdered: function() {
                return this.ordering.field == this.field;
            },
            getClass: function() {
                if (this.ordering.isDesc == true) {
                    return "fa fa-angle-down"
                } else {
                    return "fa fa-angle-up"
                }
            }
        },
        methods: {
            doCallback: function() {
                this.isDown = !this.isDown;
                this.$parent.$emit('orderChanged', { field: this.field, isDesc: this.isDown })
            },
          search: function(){
              this.$parent.$emit('searching', { field : this.field, value : this.value})
          }
        }
    }

</script>
