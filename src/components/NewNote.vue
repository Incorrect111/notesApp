<template>
  <div class="new-note">
      <label>Title</label>
    <input v-model="note.title" type="text"  />
    <label>Description</label>
    <textarea v-model="note.description"></textarea>
    <button class="btn btnPrimary" @click="addNote">New note</button>

    <div class="select">
     <select  v-model="note.priority">
              <option disabled value="">Select importance</option>
              <option>Low</option>
              <option>Medium</option>
              <option>High</option>
            </select>
            <span>{{ note.priority }}</span>
            </div>
  </div>
</template>

<script>
export default {
   props: {
     note: {
       type: Object,
       required: true
     }
   },
   methods: {
     addNote() {
       this.$emit('addNote', this.note)
     }
   }
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