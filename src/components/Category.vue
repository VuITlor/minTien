<script setup>
import { reactive, ref, onMounted } from 'vue';
import Axios from 'axios';

const products = ref([]);

onMounted( async() => {
    try {
        const response = await Axios.get('https://6721038098bbb4d93ca71a61.mockapi.io/v2/products');
        products.value = response.data;
    } catch (error) {
        console.log(error);
    }
});

</script>

<template>
    <h1 class="text-center mb-4">Danh sách sản phẩm</h1>
    <table class="table table-bordered">
        <thead class="table-dark">
            <tr>
                <th>index</th>
                <th>Name</th>
                <th>Description</th>
                <th>Price</th>
                <th>Image</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="product in products" :key="product.id">
                <td>{{ product.id }}</td>
                <td>{{ product.name }}</td>
                <td>{{ product.description }}</td>
                <td>{{ product.price }}</td>
                <td><img :src="product.image" alt="" style="width: 100px; height: 100px;"></td>
            </tr>
        </tbody>
    </table>
</template>