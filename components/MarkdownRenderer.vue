<template>
  <div v-html="$md.render(model)"></div>
</template>

<script>

export default {
  props: {content: String},
  data() {
    return{
      model: this.content
    }
  }
}

</script>
