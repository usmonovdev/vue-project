<template>
    <button 
      class="btn"
      type="button" 
      @click="onHandleFilter('all')" 
      :class="[filterName === 'all' ? 'btn-dark' : 'btn-outline-dark']"
    >
      Barcha filmlar
    </button>
</template>
<script>
export default {
    props: {
      filterName: {
        type: String,
        required: true
      },
      filterType: {
        type: String,
        required: true
      }
    }
}
</script>
<style>
    
</style>