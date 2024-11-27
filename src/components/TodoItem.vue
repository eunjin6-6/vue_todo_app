<script setup>
import { ref } from 'vue';

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
})

const isChecked = ref(props.todo.checked); //바뀔 수 있는 값으로 변경

const emit = defineEmits(['toggle-checkbox'], ['todo-delete'])

const toggleCheckbox = (e)=>{
  emit('toggle-checkbox',{
    id: props.todo.id,
    checked: e.target.checked
  })
}

const todoDelete = ()=>{
  emit('todo-delete',{
    id: props.todo.id
  })
}




</script>

<template>
  <div class="d-flex gap-2 align-items-center mt-3">
    <BFormCheckbox
      :id="`checkbox-${todo.id}`"
      v-model="isChecked"
      :name="`checkbox-${todo.id}`"
      @change="toggleCheckbox"
      >
      <!-- :class="['tab-button', { active: currentTab === tab }]" -->
      <!-- <span :class="todo.checked && 'muted'">{{ todo.title }}</span>  -->
      <span :class="{ muted: todo.checked }">{{ todo.title }}</span> 
    </BFormCheckbox>
    <BButton variant="danger" size="sm" @click="todoDelete">삭제</BButton>
  </div>
</template>

<style>
  .muted{
    text-decoration: line-through;
  }
</style>

