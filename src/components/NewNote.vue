<template lang="">
    <!-- new note -->
    <div class="new-note">
            <input v-model="note.title" type="text" />
            <textarea v-model="note.descr"></textarea>
            <button @click="addNote">New note</button>
          </div>
</template>
<script>
export default {
    props:{
      note:{
        type:Object,
        required:true,
      }
    },
    methods:{
      addNote() {
        this.$emit('addNote', this.note)
      }
    }
}
</script>
<style lang="">
    
</style>