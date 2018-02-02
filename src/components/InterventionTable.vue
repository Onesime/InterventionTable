<template>
	<div class="interventiontable">
    <Delete
      :json="json"
      style="text-align: left;">
    </Delete>
		<div class="table-responsive">
			<table class="table table-bordered table-hover">
				<thead>
					<tr>
						<th><input type="checkbox" id="check" v-on:click="checkAll()"></th>
						<THOrdering name="ID"
									field="id"
									:ordering="ordering"
										></THOrdering>
						<THOrdering name="First Name"
									field="first_name"
									:ordering="ordering"
						></THOrdering>
						<THOrdering name="Last Name"
									field="last_name"
									:ordering="ordering"
						></THOrdering>
						<THOrdering name="Email"
									field="email"
									:ordering="ordering"
						></THOrdering>
						<THOrdering name="Title"
									field="title"
									:ordering="ordering"
						></THOrdering>
						<THOrdering name="Place"
									field="place"
									:ordering="ordering"
						></THOrdering>
            			<th>Action</th>
					</tr>
				</thead>
				<tbody>
					<Row v-for="(i, index) in paginatedJson"
						:row="i"
						:key="index"
						:json="json"
						:suppr="suppr"
						:index="index">
					</Row>
          			<Create v-if="pageNumber == maxSize" :json="json"></Create>
				</tbody>
			</table>
		</div>
		<Navigation :maxSize="maxSize"
					:pageNumber="pageNumber"
					:pageChanged="pageChanged"></Navigation>
		<ModalEdit :row="selectedRow"></ModalEdit>
	</div>
</template>

<script>

import json from '../json/MOCK_DATA.json'
import Row from './Row.vue'
import Create from './Create.vue'
import Navigation from './Navigation.vue'
import THOrdering from './THOrdering.vue'
import Delete from './Delete.vue'
import ModalEdit from './ModalEdit.vue'

export default {
  	name: 'InterventionTable',
    components: {
        Row: Row,
        Create: Create,
        Navigation: Navigation,
        THOrdering: THOrdering,
        ModalEdit: ModalEdit,
        Delete: Delete
    },
    mounted() {
        this.bindEvents()
    },
	data() {
        return {
            json: json,
            pageNumber: 1,
			ordering: {
                field: 'id',
				isDesc: true,
			},
			selectedRow: json[0]
        }
    },
	props: [

  	],
	computed: {
        mounted() {
            this.bindEvents()
        },
      	sortedJson: function() {

			var me = this;
            function compare(a, b) {
                if (a[me.ordering.field] < b[me.ordering.field]) return -1;
                if (a[me.ordering.field] > b[me.ordering.field]) return 1;
                return 0;
            }

            this.json.sort(compare)
            if (this.ordering.isDesc == true) return this.json;
            return this.json.reverse();
		},
      	paginatedJson: function() {
          	return this.sortedJson.slice((this.pageNumber -1) * 10, (this.pageNumber - 1) * 10 + 10);
	  	},
        maxSize: function() {
            return Math.ceil(this.json.length / 10);
        },
	},
	methods: {
		suppr: function(index){
		  this.json.splice(index,1)
		},
  		pageChanged: function(index) {
			  if (index < 1) this.pageNumber = 1;
			  else if (index > this.maxSize - 1) this.pageNumber = this.maxSize;
			  else this.pageNumber = index;
	  	},
        bindEvents() {
            this.$on('orderChanged', (obj) => {
                this.ordering.field = obj.field;
                this.ordering.isDesc = obj.isDesc;
            })
            this.$on('selectedRowChanged', (obj) => {
                this.selectedRow = Object.assign({}, obj.row);
            })
            this.$on('rowChanged', (obj) => {
                function findRow(row) {
                    return row.id == obj.row.id;
                }
                var index = this.json.findIndex(findRow);
                this.json[index].first_name = obj.row.first_name;
                this.json[index].last_name = obj.row.last_name;
                this.json[index].email = obj.row.email;
                this.json[index].title = obj.row.title;
                this.json[index].place = obj.row.place;
                this.json[index].description = obj.row.description;
            })
        },
        checkAll: function(){
            var checkbox = Array.prototype.slice.call(document.getElementsByClassName('inputs'));
            console.log(checkbox);
            for(var i=0; checkbox[i]; ++i) {
                document.getElementById('check').checked ? checkbox[i].checked = true : checkbox[i].checked = false;
            }
        }
	},
}
</script>

<style scoped>

	.interventiontable {
		margin-left: 15%;
		width: 70%;
	}

	label {
		display: inline-block;
		width: 100%;
		height: 100%;
		padding: 0px;
		margin: 0px;
	}

	th {
		padding: 0px;
		min-width: 100px;
	}

</style>
