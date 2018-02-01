<template>
	<div class="interventiontable">
		<div class="table-responsive">
			<table class="table table-responsive">
				<thead>
					<tr>
						<th>ID</th>
						<th>First name</th>
						<th>Last name</th>
						<th>Email</th>
						<th>Title</th>
						<th>Place</th>
					</tr>
				</thead>
				<tbody>
					<Row v-for="(i, index) in paginatedJson"
						:row="i"
						:key="index">
					</Row>
				</tbody>
			</table>
		</div>
	</div>
</template>

<script>

import json from '../json/MOCK_DATA.json'
import Row from './Row.vue'

export default {
  name: 'InterventionTable',
	data() {
        return {
            json: json
        }
    },
	props: {

	},
	computed: {
      paginatedJson: function() {
          return json.slice(0, 10);
	  }
	},
    components: {
      Row: Row
    }
}
</script>

<style scoped>

</style>
