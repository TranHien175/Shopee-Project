<script setup>

import {reactive,ref,computed} from 'vue'
const message=ref('Hello World')
const state = reactive({ count: 0 })

function increment() {
  state.count++
}

const count = ref(0)
function increment2(){
    count.value++
}

const obj = reactive({
    nested: {count: 0},
    arr: ['foo','bar']
})
function mutateDeeply(){
    obj.nested.count++
    obj.arr.push('baz')
}




const author = reactive({
    name: 'John Doe',
    books: [
        'Vue 2 - Advanced Guide',
        'Vue 3 - Basic Guide',
        'Vue 4 - The Mystery'
    ]
})
const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No';
})


const isActive = ref(true)
const error = ref(null)

const classObject = computed(() => ({
  active: isActive.value && !error.value,
  'text-danger': error.value && error.value.type === 'fatal'
}))



const activeClass = ref('active')
const errorClass = ref('text-danger')

console.log(1);

const numbers = ref([1,2,3,4,5,6])
const evenNumbers = computed(()=>{
  return numbers.value.filter((n)=> n%2 ===0)
})

</script>






<template>
<h1>{{ message }}</h1>


  <button @click="increment">
    count is : {{ state.count }}
  </button>

<button @click="increment2">count is: {{count}}</button>


<h2>{{obj}}</h2>
<button @click="mutateDeeply">{{obj.nested.count}}</button>


<p>Has published books : </p>
<span>{{publishedBooksMessage}}</span>


<div :class="classObject">{{classObject}}</div>


<div :class="[activeClass, errorClass]"></div>





<li v-for="n in evenNumbers" :key="n.id">{{ n }}</li>

</template>