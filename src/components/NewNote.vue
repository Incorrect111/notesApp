<template>
  <div class="new-note">
      <label>Title</label>
    <input v-model="title.nameOfNote" type="text"/>
    <label>Description</label>
    <textarea v-model="description.descrContent"></textarea>
    <button class="btn btnPrimary" @click="addNote">New note</button>

    <div class="select">
     <select  v-model="note.priority">
              <option
              v-for="(option) in note.options"
              v-bind:value="option.value"
              :key="option.id"
               >{{ option.value }}</option>
              <!-- <option>{{ this.note.options[index] }}</option> -->
            </select>
            <span>{{ note.options.value }}</span>

            </div>
  </div>
</template>

<script>

export default {
   props: {
     note: {
       type: Object,
       required: true
     },
     title: {
       type: Object,
       required: true
     },
     description: {
       type: Object,
       required: true
     },
      options: {
      type: Array,
      required: false
    },
   },
   methods: {
     addNote() {
       this.$emit('addNote', this.note)
     }
   },
}



</script>

<style lang="scss">
.new-note   {
    text-align: center;

}
.select {
    margin-top: 25px;
    margin-bottom: -10px;
}
</style>