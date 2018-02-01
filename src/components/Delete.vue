<template>
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
