<template>
  <!-- note list -->
  <div class="notes">
    <div class="note"
      :class="[{full: !grid}, note.priority]"
      v-for="(note, index) in notes" :key="index">
      <div class="note-header" :class="{ full: !grid }">
        <p>{{ note.title }}</p>
        <p style="cursor: pointer" @click="removeNote(index)">x</p>
      </div>
      <div class="note-body">
        <p>{{ note.descr }}</p>
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    removeNote (index) {
      console.log(`Note id${index} removed`)
      this.$emit('remove', index)
    }
  }
}
</script>

<style lang="scss">
  .notes {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    padding: 40px 0;
  }
  .note {
    width: 49%;
    padding: 18px 20px;
    margin-bottom: 20px;
    background-color: #fff;
    transition: 0.25s;
    transition: all .25s cubic-bezier(.02,.01,.47,1);
    &:hover {
      box-shadow: 0 30px 30px rgba(0,0,0,0.04);
      transform: translate(0, -6px);
      transition-delay: 0s im !important;
    }
    &.full {
      width: 100%;
      text-align: center;
    }
  }
  .note-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    p {
      font-size: 22px;
      color: #444ce0;
    }
    svg {
      margin-right: 12px;
      color: #999;
      &.active {
        color: #444ce0;
      }
      &:last-child {
        margin-right: 0;
      }
    }
    &.full {
      justify-content: center;
      p {
        margin-right: 16px;
        &:last-child {
          margin-right: 0;
        }
      }
    }
  }
  .note-body {
    p {
      margin: 20px 0;
    }
    span {
      font-size: 14px;
      color: #999;
    }
  }
  .high {
    background-color: #fba94b;
  }
  .highest {
    background-color: #ff646c;
  }
</style>
