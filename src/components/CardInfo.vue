<template>
  <div class="info_popup" :class="(open)?'active':''" >
    <span @click="open = !open">&cross;</span>
    <p>Cast:</p>
      <p v-for="actor in id_cast">
        {{ actor.name }}
      </p>
    </div>
</template>
<script>
export default {
  props:{
    id_cast:{
      type: Array,
      required: true
    },
    open:{
      type: Boolean,
      required:true
    }
  }
}
</script>
<style lang="scss" scoped>
   div.info_popup{
    display: none;
    position:absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: white;
    background-color: rgba(0, 0, 0, 0.717);
    padding: 1rem;
    border-radius: 10px;
    &.active{
      display: block;
    }
  }
</style>