<script>
export default {
  props: ['modelValue'],
  emits: ['update:modelValue']
}
</script>

<template>
  <input class="styled-input"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>
<style scoped>
.styled-input{
    color: rgb(122, 124, 130);
}
</style>
