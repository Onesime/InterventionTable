<template>

    <!-- Modal -->
    <div id="myModal" class="modal fade">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Edition</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <form>
                        <div class="form-group">
                            <label for="text-input1" class="col-3 col-form-label">First name</label>
                            <div class="col-12">
                                <input class="form-control" type="text" v-model="row.first_name" id="text-input1">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="text-input2" class="col-3 col-form-label">Last name</label>
                            <div class="col-12">
                                <input class="form-control" type="text" v-model="row.last_name" id="text-input2">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="InputEmail">Email address</label>
                            <div class="col-12">
                                <input type="email" v-model="row.email" class="form-control" id="InputEmail" aria-describedby="emailHelp" placeholder="Enter email">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="text-input3" class="col-2 col-form-label">Title</label>
                            <div class="col-12">
                                <input class="form-control" type="text" v-model="row.title" id="text-input3">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="text-input4" class="col-2 col-form-label">Place</label>
                            <div class="col-12">
                                <input class="form-control" type="text" v-model="row.place" id="text-input4">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="Textarea">Description</label>
                            <textarea class="form-control" v-model="row.description" id="Textarea" rows="3"></textarea>
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-primary" v-on:click="doSubmit();">Save changes</button>
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    import ModalEdit from './ModalEdit.vue'

    export default {
        name: 'ModalEdit',
        props: [
            'row'
        ],
        methods: {
            doSubmit: function(e) {
                this.$parent.$emit('rowChanged', { row: this.row })
                $("#myModal").modal('hide')
                return true;
            }
        }
    }

</script>


