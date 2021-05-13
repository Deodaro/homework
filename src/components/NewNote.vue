<template>
  <!-- New note -->
  <div class="new-note">
    <label for="">Title</label>
    <input v-model="note.title" type="text">
    <label for="">Description</label>
    <textarea :class="[note.priority]" v-model="note.descr"></textarea>

    <!-- Priority -->
    <div class="priority-wrapper">
      <div class="priority-item">
        <p>Priority: </p>        
      </div>

      <div class="priority-item">
        <input type="radio" v-model="note.priority" name="priority" value="normal" id="normal">
        <label for="normal" >Normal</label>
      </div>

      <div class="priority-item">
        <input type="radio" v-model="note.priority" name="priority" value="high" id="high">
        <label for="high" style="color: #fba94b">High</label>
      </div>

      <div class="priority-item">
        <input type="radio" v-model="note.priority" name="priority" value="highest" id="highest">
        <label for="highest" style="color: #ff646c">Highest</label>      
      </div>
    </div>


    <!-- Priority version 2 -->
    <!-- <div class="priority-wrapper">
      <div class="priority-item">
        <p>Priority: </p>
      </div>
      <div class="priority-item"
      v-for="(option, index) in note.options"
      :key="index"> 
        <label>
          <input
          type="radio"
          v-model="note.priority"
          :value="option"
          name="priority"
          :id="index">
          {{ option }}
        </label>
      </div>
    </div> -->
    
    <button class="btn btnPrimary" @click="addNote">New Note</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      color: '',
      colors: [white, orange, red]
    } 
  },
  props: {
    note: {
      type: Object,
      required: true,
    }
  },
  methods: {
    addNote() {
      this.$emit('addNote', this.note)
    },
  }
}
</script>

<style lang="scss">
  .new-note {
    text-align: center;
  }
  .priority-wrapper {
    display: flex;
    justify-content: center;
    margin-top: 1em;
    font-size: 16px;
    .priority-item {
      display: flex;
      align-items: center;
      margin-right: 1em;
      &:last-child {
        margin-right: 0;
      }
      label {
        margin-left: 3px;
        display: flex;
        input {
          margin-left: 2px;
        }
      }
    }
  }
</style>