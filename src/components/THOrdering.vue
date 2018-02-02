<template>
    <th v-on:click="doCallback()">
        <label>{{ name }}
            <span v-if="isOrdered && ordering.isDesc"><i class="fa fa-angle-down"></i></span>
            <span v-if="isOrdered && !ordering.isDesc"><i class="fa fa-angle-up"></i></span>
        </label>
    </th>
</template>

<script>

    export default {
        name: 'THOrdering',
        props: [
            'field',
            'name',
            'ordering'
        ],
        data() {
            return {
                isDown: false,
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
                console.log("doCallback")
                this.isDown = !this.isDown;
                //console.log(this.isDown);
                this.$parent.$emit('orderChanged', { field: this.field, isDesc: this.isDown })
            }
        }
    }

</script>