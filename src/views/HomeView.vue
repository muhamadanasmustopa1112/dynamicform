<template>
  <div class="home">
    <DynamicForm />
  </div>
</template>

<script>
// @ is an alias to /src
import DynamicForm from '@/components/DynamicForm.vue'

export default {
  name: 'HomeView',
  components: {
    DynamicForm
  }
}
</script>
