<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <!-- message -->
          <message v-if="message" :message="message" />

          <!-- new note -->
          <newNote :note="note" @addNote="addNote" />

          <!-- title header -->
          <div class="note-header" style="margin-top: 30px">
            <!-- title -->
            <h1>{{ title }}</h1>
            <!-- search -->
            <search
              :value="search"
              placeholder="Find your note"
              @search="search = $event"
            />

            <!-- note icons -->
            <div class="icons">
              <svg
                :class="{ active: grid }"
                @click="grid = true"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                width="24"
                height="24"
              >
                <path fill="none" d="M0 0h24v24H0z" />
                <path
                  d="M21 3a1 1 0 0 1 1 1v16a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V4a1 1 0 0 1 1-1h18zM11 13H4v6h7v-6zm9 0h-7v6h7v-6zm-9-8H4v6h7V5zm9 0h-7v6h7V5z"
                  fill="rgba(149,164,166,1)"
                />
              </svg>
              <svg
                @click="grid = false"
                :class="{ active: !grid }"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                width="24"
                height="24"
              >
                <path fill="none" d="M0 0h24v24H0z" />
                <path
                  d="M8 4h13v2H8V4zm-5-.5h3v3H3v-3zm0 7h3v3H3v-3zm0 7h3v3H3v-3zM8 11h13v2H8v-2zm0 7h13v2H8v-2z"
                  fill="rgba(149,164,166,1)"
                />
              </svg>
            </div>
          </div>
          <!-- notes -->
          <notes :notes="notesFilter" :grid="grid" @remove="removeNote" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message.vue";
import newNote from "@/components/NewNote.vue";
import notes from "@/components/Notes.vue";
import search from "@/components/Search.vue";
import { functionTypeParam } from "@babel/types";
export default {
  components: {
    message,
    newNote,
    notes,
    search,
  },
  name: "App",
  data() {
    return {
      title: "Notes App",
      message: null,
      grid: true,
      search: "",
      note: {
        title: "",
        descr: "",
      },
      notes: [
        {
          title: "First Note",
          descr: "Description for first note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Second Note",
          descr: "Description for second note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Third Note",
          descr: "Description for third note",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    };
  },
  computed:{
    notesFilter() {
      let array = this.notes
          search = this.search
      // Small
      search = search.trim().toLowerCase()
      // Filter
      array = array.filter(function (item) {
        if(item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })

      return array
    }
  },
  methods: {
    addNote() {
      let { title, descr } = this.note;

      if (title === "") {
        this.message = `title can't be blank!`;
        return false;
      }

      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString(),
      });

      this.message = null;
      this.note.title = "";
      this.note.descr = "";
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>

<style lang="css">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}

a {
  text-decoration: none;
}

input,
textarea,
select button {
  border: 1px solid #ccc;
}

ul li {
  list-style: none;
  margin: 0;
  padding: 0;
}

.wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  margin: 0;
}

.content-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.container {
  width: 100%;
  flex: 0 0 auto;
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
}
.new-note {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  padding-top: 30px;
}
section {
  display: flex;
  justify-content: center;
  align-items: center;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-size: 30px;
  font-weight: 400;
  color: #ccc;
}
.new-note input,
.new-note textarea {
  width: 100%;
  background: #f5f5f5;
  border-radius: 20px;
  outline: none;
  height: 70px;
  text-align: center;
}
.new-note button {
  padding: 8px 25px;
  border-radius: 10px;
  border: none;
  background: rgb(27, 65, 65);
  color: #fff;
  outline: none;
  font-size: 20px;
}
</style>
