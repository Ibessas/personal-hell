<template>
  <div class="img-background">
    <div class="row flex-center">
      <div class="column flex-center">
        <q-card class="apresentation">
          <q-card-section> Nome </q-card-section>
          <q-card-section> Apresentação </q-card-section>
        </q-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>
<!-- https://unsplash.com/pt-br/fotografias/qRGuuVOzsTc -->
<style lang="sass">
.apresentation
  width: 30vw
  height: 500px
  background-color: black
.img-background
  background-image: url("https://images.unsplash.com/photo-1542228846-2d791a09d7d1?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80")
  display: block
  position: absolute
  height: 100%
  width: 100%
  background-color: black
</style>
