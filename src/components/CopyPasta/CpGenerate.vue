<template>
    <div class="cp-generate-overlay">
        <div class="cp-generate-container">
            <ul>
                <li><h3>Create Item</h3></li>
                <li><input type="text" v-model="text"></li>
                <li><button @click="handleCreate">Create</button></li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
  name: "CpGenerate",
  props: {
    
  },
  data() {
    return {
        text: ''
    }
  },
  computed: {
    
  },
  methods: {
    handleCreate() {

    }
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
