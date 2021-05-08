<template>
  <!-- new note -->
  <div class="new-note">
    <label for="">Title</label>
    <input v-model="note.title" type="text">
    <label for="">Description</label>
    <textarea :class="{ highPrior: priority === 1, highestPrior: priority === 2 }" v-model="note.descr"></textarea>
    <p> Note Priority now: {{ note.priority }} </p>

    <!-- Priority -->
    <div class="priority-wrapper">
      <div class="priority-item">
        <p>Priority: </p>
      </div>

      <div class="priority-item">
        <input type="radio" @click="note.priority = 0" v-model="note.priority" name="priority" value="normal" id="normal">
        <label for="normal" >Normal</label>
      </div>

      <div class="priority-item">
        <input type="radio" @click="this.note.priority = 1" name="priority" value="high" id="high">
        <label for="high" style="color: orange">High</label>
      </div>

      <div class="priority-item">
        <input type="radio" @click="priority = 2" name="priority" value="highest" id="highest">
        <label for="highest" style="color: red">Highest</label>      
      </div>

    </div>
    <button class="btn btnPrimary" @click="addNote">New Note</button>
  </div>
</template>

<!-- чтобы принять note в компоненте: -->
<!-- объявляем пропс  -->
<script>
export default {
  data() {
    return {
      priority: 0
    }
  },
  props: {
    note: {
      type: Object,
      required: true,
      // priority: this.note.priority
      // priority: priority
    }
  },
  // так как вызываем в компоненте метод addNote, то должны добавить methods
  // и создать там метод addNote()
  methods: {
    addNote () {
      // создаём эмит, чтобы отправлять данные из компонента родителю
      // первый параметр - название эмита, второй - то, что должно передаваться родителю
      // нам ведь нужно вернуть всю заметку в родительский компонент
      this.$emit('addNote', this.note)
    }
  }
}
</script>

<style lang="scss">
  .new-note {
    text-align: center;
    textarea {
      &.highPrior {
        background-color: orange;
      }
      &.highestPrior {
        background-color: red;
      }
    }
  }
  .priority-wrapper {
    display: flex;
    // justify-content: space-around;
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
        margin-left: 2px;
      }
    }
  }
</style>