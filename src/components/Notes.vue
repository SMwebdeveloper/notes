<template lang="">
  <!-- note list -->
  <div class="notes">
    <div class="note" :class="{full: !grid}" v-for="(note, index) in notes" :key="index">
      <div class="note-header">
        <p>{{ note.title }}</p>
        <button class="times" @click="removeNote(index)">x</button>
      </div>
      <div class="note-body">
        <p>{{ note.descr }}</p>
        <p>{{ note.date }}</p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
    grid:{
      type: Boolean,
      required:true,
    }
  },
  methods: {
    removeNote(index) {
      console.log(`Note id - ${index} removed`);
      this.$emit("remove", index);
    },
  },
};
</script>
<style lang="css">
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
  background-color: #f5f5f5;
  border-radius: 10px;
}

.note.full{
  width: 100%;
}

.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.note-header button {
  cursor: pointer;
}

.note-header p {
  font-size: 22px;
  color: #402caf;
}
.note-header .icons svg{
  width: 35px;
  height: 35px;
  margin-right: 12px;
  border:2px solid red ;
  padding: 3px;
  border-radius: 50%;
  transition: 0.3s;
  cursor: pointer;
}
.note-header .icons svg.active{
  border-color: #402caf;
}
.note-header .icons svg:last-child {
  margin-right: 0;
}
.note-body p {
  margin: 20px 0;
}
.note-body span {
  font-size: 14px;
  color: #999;
}

.times{
  border: none;
  outline: none;
  font-size: 18px;
  font-weight: 600;
  color: #402caf;
  cursor: pointer;
  transition: 0.3s;
}

.times:hover{
  color: red;
}

</style>
