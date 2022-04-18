<script setup>                         //đầu tiên cần phải khai báo các prop mà nó chấp nhận
const props = defineProps({             //defineProps : là 1 marco thời gian biên dịch mà k cần nhập
  msg: String                          //nếu ref là số thì sẽ để Number,..
})

const emit = defineEmits(['response'])             //khai báo sự kiện được phát ra

emit('response', 'hello from child')
</script>
<template>
  <h2>A Child Component!</h2>
  <h2>{{ msg || 'No props passed yet' }}</h2>

   <h2>Child component</h2>

    <slot>Fallback content</slot>
</template>