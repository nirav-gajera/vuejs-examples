<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="container">
    <h4>Vuejs Watcher Example</h4><hr style="  border: solid rgb(44, 171, 181);">
    <br>
    <h5> <i class="fa fa-comment"></i> Message length with alert :</h5>
      <input v-model="message" class="input" placeholder="Type something" />
      <p> length: {{ message.length }}</p>
  <h5> <i class="fa fa-plus"></i> Calculator :</h5>
      <input v-model="value" class="input" placeholder="Enter a value" /> &nbsp;
      <button @click="multiplyByTwo" class="btn btn-sm btn-primary ">Multiply By 2</button>
      <button @click="divide" class="btn btn-sm btn-danger">Divide By 2</button>
      <button @click="square" class="btn btn-sm btn-warning">Square</button>
      <p>Result: {{ result }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        message: '',
        value: '',
        result: '',
      };
    },
    watch: {
      message(newValue) {
        if (newValue.length > 10) {
          alert('Message is getting long! Consider shortening it.');
        }
      },
    },
    methods: {
      multiplyByTwo() {
        this.result = this.value * 2;
      },
      square() {
        this.result = this.value * this.value;
      },
      divide() {
        this.result = this.value / 2;
      },
    },
  };
  </script>
  
