<template>
  <tr>
    <td></td>
    <td class="id"></td>
    <td class="first_name"><input type="text" placeholder="first_name" v-model="first_name"/></td>
    <td class="last_name"><input type="text" placeholder="last_name" v-model="last_name"/></td>
    <td class="email"><input type="text" placeholder="email" v-model="email"/></td>
    <td class="title"><input type="text" placeholder="title" v-model="title"/></td>
    <td class="place"><input type="text" placeholder="place" v-model="place"/></td>
    <td><input type="button" class="btn btn-default" value="+" id="add" v-on:click="add"/></td>
  </tr>
</template>

<script>

export default {
  data() {
    return {
      id : "",
      first_name : "",
      last_name : "",
      email : "",
      title : "",
      place : ""
    }
  },
  name: 'Create',
  props: [
    'create',
    'json'
  ],
  methods : {
    add(){
      this.json.push({
        id : this.json.length +1,
        first_name : this.first_name,
        last_name : this.last_name,
        email : this.email,
        title : this.title,
        place : this.place
      });
    }
  }
}




</script>
