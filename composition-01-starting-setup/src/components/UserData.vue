<template>
  <div class="{class}">
    <h2>{{ uName }}</h2>
    <h3>{{ age }}</h3>
    <slot></slot>
  </div>
</template>

<script>
import {computed, inject, onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted} from 'vue';

export default {
  props: ['firstName', 'lastName'],  //age maknuto radi demonstracije
  setup(props, context) {
    const uName = computed(() => props.firstName + ' ' + props.lastName)
    
    const age = inject('userAge'); //age.value = 32 npr. bi radilo ali bi bilo nepredvidljivo i ne preporuča se. Preporuča se injectane vrijednosti mijenjati tamo od kud su provide-ane (App.vue u ovom slučaju)
    
    console.log(context);
    
    onBeforeMount(() => {
      console.log('onBeforeMount');
    })
    onMounted(() => {
      console.log('onMounted');
    })
    onBeforeUpdate(() => {
      console.log('onBeforeUpdate');
    })
    onUpdated(() => {
      console.log('onUpdated');
    })
    onBeforeUnmount(() => {
      console.log('onBeforeUnmount');
    })
    onUnmounted(() => {
      console.log('onUnmounted');
    })
    
    // context.emit('save-data', 1);
    
    return { uName, age }
  },
// computed: {
  //   userName() {
  //     return this.firstName + ' ' + this.lastName;
  //   }
  // }
}
</script>
