<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <message v-if="message" :message="message" />

          <!-- new note -->
          <newNote :note="note" @addNote="addNote" />
          <div class="note-header" style="margin: 36px 0;">

            <!-- tite -->
            <H1>{{ title }}</H1>

            <!-- search -->
            <search :value="search" placeholder="Find your note" @search="search =  $event" />

            <!-- icons controls -->
            <div class="icons">
              <svg
                :class="{ active: grid }"
                @click="grid = true"
                style="cursor: pointer"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7" />
                <rect x="14" y="3" width="7" height="7" />
                <rect x="14" y="14" width="7" height="7" />
                <rect x="3" y="14" width="7" height="7" />
              </svg>
              <svg
                :class="{ active: !grid }"
                @click="grid = false"
                style="cursor: pointer"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6" />
                <line x1="8" y1="12" x2="21" y2="12" />
                <line x1="8" y1="18" x2="21" y2="18" />
                <line x1="3" y1="6" x2="3" y2="6" />
                <line x1="3" y1="12" x2="3" y2="12" />
                <line x1="3" y1="18" x2="3" y2="18" />
              </svg>
            </div>
          </div>

          <!-- note list -->
          <notes
            :notes="notesFilter"
            @remove="removeNote"
            :grid="grid"
            :note="note"
          />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message.vue";
import notes from "@/components/Notes.vue";
import newNote from "@/components/NewNote.vue";
import search from "@/components/Search.vue";

export default {
  components: {
    message,
    notes,
    newNote,
    search
  },

  data() {
    return {
      title: "Notes app",
      search: "",
      message: null,
      grid: true,

      note: {

        title: "",

        description: "",

        priority: "",

        highPriority: false,

        mediumPriority: false,

        lowPriority: false,

        hidenTitle: false,

        titleShow: true,

        titleEditing: 'titleEditing',

        descrEditing: 'descrEditing',

        additionalTitleVar: "",

        hidenDescr: false,

        descrShow: true,

        additionalDescrVar: ""
      },

      notes: [
        {
          title: "First note",

          description: "Description for first note",

          date: new Date(Date.now()).toLocaleString(),

          priority: "",

          highPriority: false,

          mediumPriority: false,

          lowPriority: false,

          hidenTitle: false,

          titleShow: true,

          additionalTitleVar: "",

          hidenDescr: false,

          descrShow: true,

          additionalDescrVar: "",

          titleEditing: "titleEditing",

          descrEditing: 'descrEditing',

        },

        {
          title: "Second note",

          description: "Description for Second note",

          date: new Date(Date.now()).toLocaleString(),

          priority: "",

          highPriority: false,

          mediumPriority: false,

          lowPriority: false,

          hidenTitle: false,

          titleShow: true,

          additionalTitleVar: "",

          hidenDescr: false,

          descrShow: true,

          additionalDescrVar: "",

          titleEditing: "titleEditing",

          descrEditing: 'descrEditing',

        },

        {
          title: "Third note",

          description: "Description for Third note",

          date: new Date(Date.now()).toLocaleString(),

          priority: "",

          highPriority: false,

          mediumPriority: false,

          lowPriority: false,

          hidenTitle: false,

          titleShow: true,

          additionalTitleVar: "",

          hidenDescr: false,

          descrShow: true,

          additionalDescrVar: "",

          titleEditing: "titleEditing",

          descrEditing: 'descrEditing',

        }
      ]
    };
  },

  computed: {
    notesFilter() {
      let array = this.notes,
        search = this.search;

      if (!search) return array;

      // Lower case
      search = search.trim().toLowerCase();

      // Filter
      array = array.filter(function(item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });

      // Error
      return array;
    }
  },

  methods: {
    addNote() {
      console.log(this.note);

      let {
        title,
        description,
        priority,
        red,
        blue,
        highPriority,
        mediumPriority,
        lowPriority,
        hidenTitle,
        titleShow,
        additionalTitleVar,
        hidenDescr,
        descrShow,
        additionalDescrVar,
        titleEditing,
        descrEditing
      } = this.note;

      if (title === "") {
        this.message = "title can`t be blank!";
        return false;
      }

      switch (priority) {
        case "High":
          highPriority = true;
          break;

        case "Medium":
          mediumPriority = true;
          break;

        case "Low":
          lowPriority = true;
          break;
      }

      this.notes.push({
        title,
        description,
        priority,
        highPriority,
        mediumPriority,
        lowPriority,
        hidenTitle,
        titleShow,
        additionalTitleVar,
        hidenDescr,
        descrShow,
        additionalDescrVar,
        titleEditing,
        descrEditing,
        date: new Date(Date.now()).toLocaleString()
      });

      (this.note.title = ""),
        (this.note.description = ""),
        (this.note.priority = undefined);
      this.message = null;
    },

    // Remove note

    removeNote(index) {
      this.notes.splice(index, 1);
    },
  }
};
</script>

<style>
</style>
