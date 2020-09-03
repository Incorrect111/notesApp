<template>
  <div class="notes">
    <div
      class="note"
      :class="[note.priority, {full: !grid}]"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note-header">
        <p
          style="cursor: pointer"
          v-show="note.titleShow"
          @click="editing(index, note.titleEditing)"
        >{{ note.nameOfNote }}</p>
        <br />
        <br />
        <input v-model="note.additionalTitleVar" v-show="note.hidenTitle" />
        <p style="cursor: pointer" @click="removeNote(index)">x</p>
      </div>

      <div class="note-body">
        <p
          style="cursor: pointer"
          v-show="note.descrShow"
          @click="editing(index, note.descrEditing)"
        >{{ note.descrContent }}</p>
        <input v-model="note.additionalDescrVar" v-show="note.hidenDescr" />
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },

  props: {
    notes: {
      type: Array,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    },
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
    }
  },
  methods: {
    // Remove note
    removeNote(index) {
      this.$emit("remove", index);
    },

    //Editing note
    editing(index, editParam) {
      if (editParam === "titleEditing") {
        this.notes[index].titleShow = false;
        this.notes[index].additionalTitleVar = this.notes[index].nameOfNote;
        this.notes[index].hidenTitle = true;

        document.body.addEventListener("keyup", e => {
          if (e.keyCode === 13) {
            this.notes[index].hidenTitle = false;
            this.notes[index].titleShow = true;
            this.notes[index].nameOfNote = this.notes[index].additionalTitleVar;
          } else if (e.keyCode === 27) {
            this.notes[index].hidenTitle = false;
            this.notes[index].titleShow = true;
          }
        });
      } else if (editParam === "descrEditing") {
        this.notes[index].descrShow = false;
        this.notes[index].additionalDescrVar = this.notes[index].descrContent;
        this.notes[index].hidenDescr = true;
        document.body.addEventListener("keyup", e => {
          if (e.keyCode === 13) {
            this.notes[index].hidenDescr = false;
            this.notes[index].descrShow = true;
            this.notes[index].descrContent = this.notes[index].additionalDescrVar;
          } else if (e.keyCode === 27) {
            this.notes[index].hidenDescr = false;
            this.notes[index].descrShow = true;
          }
        });
      }
    }
  }
};
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #fff;

  &.full {
    width: 100%;
  }
  &.High {
    border: solid;
    border-color: rgb(255, 0, 0);
  }

  &.Medium {
    border: solid;
    border-color: rgb(235, 231, 12);
  }
  &.Low {
    border: solid;
    border-color: rgb(138, 124, 124);
  }
}

.note-body {
  p {
    margin: 20px 0px;
  }
  span {
    font-size: 14px;
    color: #999999;
  }
}
.note-header {
  display: flex;
  text-align: center;
  justify-content: space-between;

  p {
    font-size: 22px;
    color: rgb(45, 30, 255);
  }
}

svg {
  margin-right: 12px;
  color: #999999;
  &.active {
    color: blue;
  }

  &:last-child {
    margin-right: 0;
  }
}
</style>