<template>
    <i :class="iconClasses"></i>
</template>
  
<script>
export default {
    name: 'MyIcon',
    props: {
        name: {
            type: String,
            required: true
        },
        size: {
            type: String,
            default: '24px'
        },
        color: {
            type: String,
            default: 'currentColor'
        }
    },
    computed: {
        iconClasses() {
            return 'mdi ' + this.name
        },
        iconStyles() {
            return {
                fontSize: this.size,
                color: this.color
            }
        }
    }
}
</script>
  
<style></style>