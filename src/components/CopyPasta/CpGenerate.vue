<template>
    <div class="cp-generate-overlay" v-if="activate">
        <div class="cp-generate-container">
            <h3>Enter input title</h3>
            <slot name="input"></slot>
        </div>
    </div>
</template>

<script>
export default {
  name: "CpGenerate",
  props: {
    activate: {
        type: Boolean,
        default: false
    }
  },
  data() {
    return {
        
    }
  },
  computed: {
    
  },
  methods: {
    
  },
  created() {
    
  }
};
</script>

<style>
    .cp-generate-overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 2;
        background-color: rgba(33, 33, 33, 0.3);
    }
    .cp-generate-container {
        background-color: white;
        padding: 20px;
        width: 300px;
        box-shadow: 0 3px 1px -2px rgb(0 0 0 / 20%), 0 2px 2px 0 rgb(0 0 0 / 14%), 0 1px 5px 0 rgb(0 0 0 / 12%);
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    }
</style>
