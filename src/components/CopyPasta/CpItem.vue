<template>
    <li>
        <button @click.prevent="handleCopy" class="normal">Copy</button>
        <div class="text-area-wrap">
            <label>{{ inputText.title ? inputText.title : 'Title' }}</label>
            <textarea name="" id="" cols="10" rows="1" v-model="inputText.text" @change="handleOnChange"></textarea>
        </div>
        <button @click.prevent="handleDelete" class="danger">Remove</button>
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

<style>
    
</style>
