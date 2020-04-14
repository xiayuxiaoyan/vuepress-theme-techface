<template>
  <div>
    <p><router-link to="pg1"> to pg1</router-link></p>
    <p><router-link to="pg1-1"> to pg1-1</router-link></p>
    we are in {{key}}
  </div>
</template>

<script>
function getKey(path){
  return path.includes('pg1-1') ? 'pg1-1' : 'pg1';
}
export default {
  mounted(){
    this.$nextTick()
      .then(() => {
        this.key = getKey(this.$route.path);
      })
  },
  data(){
    return{
      key: '',
    }
  },
}
</script>