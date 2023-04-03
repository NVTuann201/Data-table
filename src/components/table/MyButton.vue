<template>
  <button :class="buttonClasses">
    <MyIcon :name="icon"></MyIcon>
    {{ label }}
  </button>
</template>

<script>
import MyIcon from "./MyIcon.vue";
export default {
  name: "MyButton",
  components: { MyIcon },
  props: {
    icon: {
      type: String,
    },
    label: {
      type: String,
      required: true,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    primary: {
      type: Boolean,
      default: false,
    },
    danger: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    buttonClasses() {
      return {
        button: true,
        "button-primary": this.primary,
        "button-danger": this.danger,
        "button-disabled": this.disabled,
      };
    },
  },
  methods: {
    // handleClick() {
    //     if (!this.disabled) {
    //         this.$emit('click');
    //     }
    // }
  },
};
</script>

<style scoped></style>
