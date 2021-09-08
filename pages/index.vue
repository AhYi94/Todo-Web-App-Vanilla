<template>
  <div class="mx-20">
    <div class="flex justify-between my-5">
      <div class="my-5 w-1/3">
        <div class="flex">
          <input
            v-model="newItem.name"
            class="
              shadow
              appearance-none
              border
              rounded
              w-full
              py-2
              px-3
              text-gray-700
              leading-tight
              focus:outline-none focus:shadow-outline
            "
          />
          <button
            @click="addItem"
            class="
              bg-green-500
              hover:bg-green-700
              text-white
              font-bold
              w-1/4
              py-1
              px-1
              ml-5
              rounded
            "
          >
            Add Project
          </button>
        </div>
      </div>

      <div>
        <div class="ml-auto text-center">
          <label class="uppercase font-bold"> Total </label>
          <div class="shadow-inner text-center p-2 bg-white">
            <b>{{ totalItems }}</b> <br />Projects
          </div>
        </div>
      </div>
    </div>
    <div class="flex justify-between">
      <todo-draggable title="To Do" :items="items" :list="1" />
      <todo-draggable title="In Progress" :items="items" :list="2" />
      <todo-draggable title="Done" :items="items" :list="3" />
    </div>
  </div>
</template>

<script>
import TodoDraggable from '~/components/TodoDraggable.vue'
export default {
  data() {
    return {
      items: [
        { name: 'Project 1', id: 1, list: 1 },
        { name: 'Project 2', id: 2, list: 1 },
        { name: 'Project 3', id: 3, list: 1 },
        { name: 'Project 4', id: 4, list: 1 },
        { name: 'Project 5', id: 5, list: 2 },
        { name: 'Project 6', id: 6, list: 2 },
        { name: 'Project 7', id: 7, list: 3 },
        { name: 'Project 8', id: 8, list: 3 },
        { name: 'Project 9', id: 9, list: 3 },
      ],
      newItem: { name: null, id: null, list: null },
    }
  },
  components: { TodoDraggable },
  computed: {
    totalItems() {
      return this.items.length
    },
  },
  methods: {
    addItem() {
      if (!this.newItem.name) {
        alert("Title shouldn't be empty")
        return
      }
      this.newItem.id = this.items.length + 1
      this.newItem.list = 1
      this.items.push({ ...this.newItem })
      this.newItem.name = null
    },
  },
}
</script>
