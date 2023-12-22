<template>
  <div class="info_popup" :class="(open)?'active':''" >
    <span @click="open = !open">&cross;</span>
    <h4>Cast:</h4>
      <p v-for="actor in id_cast">
        {{ actor.name }}
      </p>
      <h4>Generi:</h4>
      <p v-for="genre in genres.slice(0, 5)">
        {{ genre.name }}
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
    genres:{
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

    h4{
      margin: .5rem 0;
    }
  }
</style>