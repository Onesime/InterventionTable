<template>
    <form class="form-inline" v-on:submit="doCallback">
        <div class="form-group">
            <label for="search-input" class="col-2 col-form-label">Search</label>
            <div class="col-10">
                <input class="form-control" type="search" v-model="value" id="search-input" v-on:keyup="doCallback">
            </div>
        </div>
    </form>
</template>

<script>

    export default {
        name: 'Search',
        data() {
            return {
                value: '',
            }
        },
        methods: {
            doCallback: function() {
                this.$parent.$emit('globalSearch', this.value)
            }
        }
    }

</script>