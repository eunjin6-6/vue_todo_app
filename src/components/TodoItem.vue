<script setup>
import { ref } from 'vue';

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
})

const isChecked = ref(props.todo.checked); //바뀔 수 있는 값으로 변경

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
      v-model="isChecked"
      name="checkbox-1"
      value="accepted"
      unchecked-value="not_accepted"
      @change="toggleCheckbox"
      >
      <!-- :class="['tab-button', { active: currentTab === tab }]" -->
      <!-- <span :class="todo.checked && 'muted'">{{ todo.title }}</span>  -->
      <span :class="{ muted: todo.checked }">{{ todo.title }}</span> 
    </BFormCheckbox>
  </div>
</template>

<style>
  .muted{
    text-decoration: line-through;
  }
</style>

