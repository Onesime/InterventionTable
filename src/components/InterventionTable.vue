<template>
	<div class="interventiontable">
		<div class="table-responsive">
			<table class="table">
				<thead>
					<tr>
						<th>ID</th>
						<th>First name</th>
						<th>Last name</th>
						<th>Email</th>
						<th>Title</th>
						<th>Place</th>
            			<th>Action</th>
					</tr>
				</thead>
				<tbody>
					<Row v-for="(i, index) in paginatedJson"
						:row="i"
						:key="index">
					</Row>
          			<Create v-if="pageNumber == maxSize" :json="json"></Create>
				</tbody>
			</table>
		</div>
		<Navigation :maxSize="maxSize"
					:pageNumber="pageNumber"
					:pageChanged="pageChanged"></Navigation>
	</div>
</template>

<script>

import json from '../json/MOCK_DATA.json'
import Row from './Row.vue'
import Create from './Create.vue'
import Navigation from './Navigation.vue'

export default {
  name: 'InterventionTable',
	data() {
        return {
            json: json,
            pageNumber: 1,
        }
    },
	props: {

	},
	computed: {
      	paginatedJson: function() {
          	return this.json.slice((this.pageNumber -1) * 10, (this.pageNumber - 1) * 10 + 10);
	  	},
        maxSize: function() {
            return Math.ceil(this.json.length / 10);
        },
	},
    components: {
      	Row: Row,
      	Create: Create,
        Navigation: Navigation
	},
	methods: {
      pageChanged: function(index) {
          if (index < 1) this.pageNumber = 1;
          else if (index > this.maxSize - 1) this.pageNumber = this.maxSize;
          else this.pageNumber = index;
	  }
	}
}
</script>

<style scoped>

	.interventiontable {
		margin-left: 20%;
		width: 60%;
	}

</style>
