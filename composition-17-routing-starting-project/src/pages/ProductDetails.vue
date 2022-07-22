<template>
  <section>
    <h2>{{ title }}</h2>
    <h3>${{ price}}</h3>
    <p>{{ description}}</p>
  </section>
</template>

<script>
import { ref, inject } from 'vue';

export default {
  setup(props) {
    const products = inject('products');
    console.log(products);
    
    const title = ref('');
    const price = ref(null);
    const description = ref('');
    
    const selectedProduct = products.find(product => {
      return product.id===props.pid;
    });  //products id equal to passed router p-id.
    console.log(selectedProduct);

    return { title, price, description };
  },
};
</script>


<style scoped>
section {
  margin: 3rem auto;
  max-width: 40rem;
  padding: 1rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
}
</style>