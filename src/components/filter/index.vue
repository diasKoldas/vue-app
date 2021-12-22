<template>
  <div class="filterWrapper">
    <div class="filterTitle">
      <span>{{title}}</span>
      <button>
        <img :src="close" alt="">
      </button>
    </div>
    <div class="filterOptions">
      <div
          v-for="(option, key) in options"
          class="filterOptionsItem"
          v-bind:key="key"
      >
        <input  :value="key" :name="key" type="checkbox" :id="key" v-model="selectedOptions" @change="onChange">
        <label :for="key">{{option}}</label>
      </div>
    </div>
  </div>
</template>

<script>
import close from '../../assets/close-icon.png';
export default {
  name: 'Filter',
  props: {
    title: String,
    options: Object,
  },
  data: () => ({
    close,
    selectedOptions: []
  }),
  methods: {
    onChange() {
      this.$emit('select', this.selectedOptions);
    },
    clearAll(){
      this.selectedOptions = [];
    }
  }
}
</script>

<style src="./Filter.css"/>