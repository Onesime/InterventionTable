<template>
	<div class="interventiontable">
		<h1>Intervention table</h1>
        <form class="form-inline search_group">
            <Search></Search>
            <Delete
              :json="json">
            </Delete>
        </form>
		<div class="table-responsive">
			<table class="table table-bordered table-hover">
				<thead>
					<tr>
						<th class="checkbox"><input type="checkbox" id="check" v-on:click="checkAll()"></th>
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
            			<th class="buttons">Action</th>
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
import Search from './Search.vue'

export default {
  	name: 'InterventionTable',
    components: {
        Row: Row,
        Create: Create,
        Navigation: Navigation,
        THOrdering: THOrdering,
        ModalEdit: ModalEdit,
        Delete: Delete,
        Search: Search,

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
        searching: {
              field: '',
              value: ''
        },
			selectedRow: json[0],
			globalSearchValue: ''
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
            function globalSearch(obj) {
                if ((obj.id + '').indexOf(me.globalSearchValue) != -1) return true;
                if ((obj.last_name.toLowerCase() + '').indexOf(me.globalSearchValue.toLowerCase()) != -1) return true;
                if ((obj.first_name.toLowerCase() + '').indexOf(me.globalSearchValue.toLowerCase()) != -1) return true;
                if ((obj.email.toLowerCase() + '').indexOf(me.globalSearchValue.toLowerCase()) != -1) return true;
                if ((obj.title.toLowerCase() + '').indexOf(me.globalSearchValue.toLowerCase()) != -1) return true;
                if ((obj.place.toLowerCase() + '').indexOf(me.globalSearchValue.toLowerCase()) != -1) return true;
                if ((obj.description.toLowerCase() + '').indexOf(me.globalSearchValue.toLowerCase()) != -1) return true;
                return false;
            }

            var found = [];
            if (this.globalSearchValue.length != 0) {
                found = this.json.filter(globalSearch);
            } else {
                found = this.json;
            }

            if (found == undefined) found = this.json;
            else if (found.length == undefined) found = this.json;

                  function compare(a, b) {
                      if (a[me.ordering.field] < b[me.ordering.field]) return -1;
                      if (a[me.ordering.field] > b[me.ordering.field]) return 1;
                      return 0;
                  }

                  function search(a){
                    return ((a[me.searching.field] + '').toLowerCase() + '').indexOf(me.searching.value.toLowerCase()) != -1;
                  }

            if (this.searching.value.length != 0) {
              found = found.filter(search);
            }
            found.sort(compare)
            if (this.ordering.isDesc == true) return found;
            return found.reverse();
		    },
      	paginatedJson: function() {
            var number = 10;
            if(screen.width <= 480){
              number = 5;
            }
          	return this.sortedJson.slice((this.pageNumber -1) * number, (this.pageNumber - 1) * number + number);
	  	},
        maxSize: function() {
          var number = 10;
          if(screen.width <= 480){
            number = 5;
          }
          return Math.ceil(this.sortedJson.length / number);
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
                this.ordering = obj
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
            this.$on('globalSearch', (value) => {
                this.globalSearchValue = value
            })
            this.$on('searching', (obj) => {
              this.searching.field = obj.field
              this.searching.value = obj.value
            })
        },
        checkAll: function(){
            var checkbox = Array.prototype.slice.call(document.getElementsByClassName('inputs'));
            for(var i=0; checkbox[i]; ++i) {
                document.getElementById('check').checked ? checkbox[i].checked = true : checkbox[i].checked = false;
            }
        }
	},
}
</script>

<style scoped>

</style>
