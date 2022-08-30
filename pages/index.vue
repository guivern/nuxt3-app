<template>
  <main>
    <h1>Index Page</h1>
    <table border="1 px solid" v-if="data">
      <thead>
        <tr>
          <th>Name</th>
          <th>Symbol</th>
          <th>Price</th>
          <th>Details</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="currency in data.data" :key="currency.id">
          <td>{{ currency.name }}</td>
          <td>{{ currency.symbol }}</td>
          <td>{{ currency.price_usd }}</td>
          <td>
            <NuxtLink :to="'/currency/' + currency.id">{{
              currency.id
            }}</NuxtLink>
          </td>
        </tr>
      </tbody>
    </table>
    The count is: {{ count }}
    <button @click="addCount">Add count</button>
  </main>
</template>
<script setup>
const { data } = await useFetch('/api/tickers?limit=10');
const count = ref(1);

function addCount() {
  count.value++;
}

watch(count, (currentValue, oldValue) => {
  console.log(oldValue, currentValue);
});
</script>
