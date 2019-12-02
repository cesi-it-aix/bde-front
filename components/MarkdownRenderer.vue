<template>
  <div v-html="$md.render(model)"></div>
</template>

<script>
// ajouter une query que l'on donnera a markdown
var mardown = '# Hello World!'

export default {
  data() {
    return {
      model: mardown
    }
  }
}
</script>
