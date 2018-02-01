<template>
    <nav aria-label="Page navigation example">
        <ul class="pagination justify-content-center">
            <li class="page-item"><a class="page-link" v-on:click="changePage(1)">Begin</a></li>
            <li class="page-item"><a class="page-link" v-on:click="changePage(pageNumber - 1)">Previous</a></li>
            <li v-if="maxSize <= 10" v-for="n in maxSize" class="page-item"><a class="page-link" v-on:click="changePage(n)">{{ n }}</a></li>
            <li v-if="maxSize > 10" v-for="n in getBegin" class="page-item"><a class="page-link 1" v-on:click="changePage(n)">{{ n }}</a></li>
            <li v-if="maxSize > 10" class="page-item active"><a class="page-link 2" v-on:click="changePage(pageNumber)">{{ pageNumber }}</a></li>
            <li v-if="maxSize > 10" v-for="n in getEnd" class="page-item"><a class="page-link 3" v-on:click="changePage(n)">{{ n }}</a></li>
            <li class="page-item"><a class="page-link" v-on:click="changePage(pageNumber + 1)">Next</a></li>
            <li class="page-item"><a class="page-link" v-on:click="changePage(maxSize)">End</a></li>
        </ul>
    </nav>
</template>

<script>

    export default {
        name: 'Row',
        props: [
            'maxSize', "pageNumber", "pageChanged",
        ],
        methods: {
            changePage: function(index) {
                this.pageChanged(index);
            }
        },
        computed: {
            getBegin: function() {
                var x = this.pageNumber - 5;
                if (x <= 1) x = 1;

                var arr = [];
                for (var i = x; i < this.pageNumber; i++) {
                    arr.push(i);
                }
                return arr;
            },
            getEnd: function() {
                if (this.pageNumber >= this.maxSize) return 0;

                var arr = [];
                for (var i = this.pageNumber + 1; i < this.pageNumber + 6; i++) {
                    if (i > this.maxSize) break;
                    arr.push(i);
                }
                return arr;
            }
        }
    }

</script>

<style scoped>

</style>