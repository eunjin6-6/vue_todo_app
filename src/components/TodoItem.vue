<script setup>
const props = defineProps({
  todo: {
    type: String,
    required: true,
  },
})


const emit = defineEmits(['toggle-checkbox'])

const toggleCheckbox = (e)=>{
  emit('toggle-checkbox',{
    id: props.todo.id,
    checked: e.target.checked
  })
}


</script>

<template>
  <div>
    <BFormCheckbox
      id="checkbox-1"
      v-model="status"
      name="checkbox-1"
      value="accepted"
      unchecked-value="not_accepted"
      @change="toggleCheckbox"
      >
      <!-- :class="['tab-button', { active: currentTab === tab }]" -->
      <span :class="todo.checked && 'muted'">{{ todo.title }}</span> 
    </BFormCheckbox>
  </div>
</template>

<style>
  .muted{
    text-decoration: line-through;
  }
</style>

