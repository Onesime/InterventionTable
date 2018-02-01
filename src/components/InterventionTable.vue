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
					<tr v-for="i in paginatedJson">
						<td>{{ i.id}}</td>
						<td>{{ i.first_name}}</td>
						<td>{{ i.last_name}}</td>
						<td>{{ i.email}}</td>
						<td>{{ i.title}}</td>
						<td>{{ i.place}}</td>
					</tr>
				</tbody>
			</table>
		</div>
	</div>
</template>

<script>

import json from '../json/MOCK_DATA.json'

export default {
  name: 'InterventionTable',
	data() {
        return {
            json: json
        }
    },
	computed: {
      paginatedJson: function() {
          return json.slice(0, 10);
	  }
	}
}
</script>

<style scoped>

</style>
