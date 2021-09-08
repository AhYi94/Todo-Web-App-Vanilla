<!-- Please remove this file from your project -->
<template>
  <div
    class="w-1/5"
    @drop="onDrop($event, list)"
    @dragover.prevent
    @dragenter.prevent
  >
    <div class="bg-gray-500 p-4 flex justify-between">
      <h1 class="text-white text-2xl self-center">{{ title }}</h1>
      <div class="shadow-inner text-center p-2 bg-white">
        <b>{{ countListItem }}</b> <br />Projects
      </div>
    </div>
    <div
      v-for="element in listItem"
      :key="element.id"
      draggable="true"
      class="bg-white p-5 border-b-2 break-all"
      @dragstart="startDrag($event, element)"
    >
      {{ element.name }}
    </div>
  </div>
</template>
<script>
export default {
  props: {
    title: { String, default: '' },
    items: { Object, default: [] },
    list: { Number, default: null },
  },

  computed: {
    listItem() {
      return this.items.filter((item) => item.list === this.list)
    },
    countListItem() {
      const total = this.items.filter((item) => item.list === this.list)
      return total.length
    },
  },
  methods: {
    startDrag: (evt, item) => {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemID', item.id)
    },
    onDrop(evt, list) {
      const itemID = evt.dataTransfer.getData('itemID')
      const item = this.items.find((item) => item.id === parseInt(itemID))
      item.list = list
    },
  },
}
</script>
