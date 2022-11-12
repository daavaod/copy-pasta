<template>
    <li>
        <button @click.prevent="handleCopy">Copy</button>
        <textarea name="" id="" cols="30" rows="10" v-model="inputText.text" @change="handleOnChange"></textarea>
        <button @click.prevent="handleDelete">Delete</button>
    </li>
</template>

<script>
export default {
  name: "CpItem",
  props: {
    itemData: {
        type: Object,
        default: null
    }
  },
  data() {
    return {
        inputText: {}
    }
  },
  computed: {
    
  },
  methods: {
    handleCopy() {
        this.$emit('emitInput', this.inputText.text)
        navigator.clipboard.writeText(this.inputText.text)
    },
    handleDelete() {
        this.$emit('emitDelete', this.inputText.id)
    },
    handleOnChange() {
        this.$emit('emitChange', this.inputText)
    }
  },
  created() {
    this.inputText = this.itemData;
  }
};
</script>

<style scoped>
    
</style>
