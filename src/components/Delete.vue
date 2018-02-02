<template>
  <div style="float:left">
    <input type="button" class="btn btn-danger" value="Delete" v-on:click="supprCheck()"/>
  </div>
</template>

<script>
  export default {
    name: 'Delete',
    props: [
      'json',
    ],
    methods: {
      supprCheck: function () {
        var checkbox = Array.prototype.slice.call(document.getElementsByClassName('inputs'));
        for(var i=0; checkbox[i]; ++i){
            if(checkbox[i].checked){
              var id = checkbox[i].id.replace( /^\D+/g, '');
              var j = 0;
              while (j < this.json.length - 1) {
                if (this.json[j].id == id) {
                  this.json.splice(j,1);
                  break;
                }
                j = j + 1;
              }
            }
        }
        for(var i=0; checkbox[i]; ++i) {
          if (checkbox[i].checked) {
            checkbox[i].checked = false;
          }
        }
        var checkAll = document.getElementById('check');
        checkAll.checked ? checkAll.checked = false : "";
      }
  }
  }

</script>
