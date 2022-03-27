<template>
  <div class="note-badge">
    <span
      :class="[
        'badge-container',
        note * 10 < 25 ? 'badge-danger' : 'badge-medium',
      ]"
      v-if="note * 10 < 50"
    >
      <span>{{ note * 10 }}<small>%</small></span></span
    >
    <span
      :class="[
        'badge-container',
        note * 10 < 75 ? 'badge-better' : 'badge-best',
      ]"
      v-else
    >
      <span>{{ note * 10 }}<small>%</small></span></span
    >
  </div>
</template>

<script>
export default {
  name: 'Note',
  props: {
    note: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {};
  },
  methods: {
    // getDefaultStyle() {
    //   const border = this.calculateNoteStyle();
    //   console.log(border);
    //   return {
    //     border,
    //     display: 'inline-flex',
    //     width: '90%',
    //     height: '90%',
    //     borderRadius: '50%',
    //     padding: '1em',
    //     justifyContent: 'center',
    //     alignItems: 'center',
    //     transform: 'rotate(45deg)',
    //   };
    // },
    // calculateNoteStyle() {
    //   const note = this.note * 10;
    //   if (note < 25) {
    //     return {
    //       borderTop: 'solid 3px #e03030;',
    //     };
    //   } else if (note < 50) {
    //     return {
    //       borderTop: 'solid 3px #e68026;',
    //       borderRight: 'solid 3px #e68026;',
    //     };
    //   } else if (note < 75) {
    //     return {
    //       borderTop: 'solid 3px #ebeb32;',
    //       borderRight: 'solid 3px #ebeb32;',
    //       borderBottom: 'solid 3px #ebeb32;',
    //     };
    //   } else {
    //     console.log(note);
    //     return {
    //       borderTop: 'solid 3px #2cc714;',
    //       borderRight: 'solid 3px #2cc714;',
    //       borderBottom: 'solid 3px #2cc714;',
    //       borderLeft: 'solid 3px #2cc714;',
    //     };
    //   }
    // },
  },
  created() {
    // console.log(this.note);
    // this.calculateNoteStyle(this.note * 10);
  },
};
</script>

<style lang="scss" scoped>
.note-badge {
  display: inline-flex;
  position: absolute;
  bottom: -20px;
  left: 10px;
  width: 50px;
  height: 50px;
  //   padding: 1.8em;
  border-radius: 50%;
  background-color: #1d1a1a;
  color: rgb(223, 212, 212);
  align-items: center;
  justify-content: center;
  font-size: 0.9em;
  font-weight: 600;
  //   border: solid 3px #2cc714;
  .badge-container {
    display: inline-flex;
    width: 90%;
    height: 90%;
    border-radius: 50%;
    padding: 1em;
    justify-content: center;
    align-items: center;
    transform: rotate(45deg);
    // border-top: solid 3px #e03030;
    // border-right: solid 3px #e68026;
    // border-bottom: solid 3px #2cc714;
    // border-left: solid 3px #ebeb32;
    // &::before {
    //   content: '';
    //   position: absolute;
    //   box-sizing: content-box;
    //   top: -3px;
    //   left: -3px;
    //   width: 100%;
    //   height: 100%;
    //   border-radius: 50%;
    //   background-color: transparent;
    //   border: solid 3px transparent;
    //   border-left: solid 3px #5610c5;
    //   transform: rotate(90deg);
    // }
    // &::after {
    //   content: '';
    //   position: absolute;
    //   box-sizing: content-box;
    //   top: -3px;
    //   left: -3px;
    //   width: 100%;
    //   height: 100%;
    //   border-radius: 50%;
    //   background-color: transparent;
    //   border: solid 3px transparent;
    //   border-top: solid 3px #2cc714;
    //   transform: rotate(0deg);
    // }
    span {
      transform: rotate(-45deg);
    }
  }
  .badge-danger {
    border: solid 3px #e03030;
  }
  .badge-medium {
    border: solid 3px #e68026;
  }
  .badge-better {
    border: solid 3px #ebeb32;
  }
  .badge-best {
    border: solid 3px #2cc714;
  }
}
</style>
