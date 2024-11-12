<script setup>
import { reactive, ref, onMounted } from 'vue';
import Axios from 'axios';

const products = reactive([]);

const name = ref('');
const description = ref('');
const price = ref('');
const image = ref('');

onMounted(async () => {
    try {
        const response = await Axios.get('https://6721038098bbb4d93ca71a61.mockapi.io/v2/products');
        if (response.status === 200) {
            products.push(...response.data);
        }
    } catch (error) {
        console.log(error);
    }
});

const addProduct = async () => {
    try {
        const response = await Axios.post('https://6721038098bbb4d93ca71a61.mockapi.io/v2/products', {
            name: name.value,
            description: description.value,
            price: price.value,
            image: image.value
        });
        if (response.status === 201) {
            products.push(response.data);
        }
    } catch (error) {
        console.log(error);
    }

    name.value = '';
    description.value = '';
    price.value = '';
    image.value = '';
};

const deleteProduct = async (id) => {
    try {
        const response = await Axios.delete(`https://6721038098bbb4d93ca71a61.mockapi.io/v2/products/${id}`);
        if (response.status === 200) {
            products.splice(products.findIndex(product => product.id === id), 1);
        }
    } catch (error) {
        console.log(error);
    }
}
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
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="product in products" :key="product.id">
                <td>{{ product.id }}</td>
                <td>{{ product.name }}</td>
                <td>{{ product.description }}</td>
                <td>{{ product.price }}</td>
                <td><img :src="product.image" alt="" style="width: 100px; height: 100px;"></td>
                <td>
                    <button @click="deleteProduct(product.id)" class="btn btn-danger btn-sm">Delete</button>
                </td>
            </tr>
        </tbody>
    </table>

    <div class="form-add mx-auto mb-5 mt-3" style="width: 500px;">
        <h2>Add Product</h2>
        <form>
            <div class="mb-3">
                <label for="name" class="form-label">Name</label>
                <input type="text" v-model="name" class="form-control" id="name" placeholder="Enter name">
            </div>
            <div class="mb-3">
                <label for="description" class="form-label">Description</label>
                <input type="text" v-model="description" class="form-control" id="description"
                    placeholder="Enter description">
            </div>
            <div class="mb-3">
                <label for="price" class="form-label">Price</label>
                <input type="text" v-model="price" class="form-control" id="price" placeholder="Enter price">
            </div>
            <div class="mb-3">
                <label for="image" class="form-label">Image</label>
                <input type="text" v-model="image" class="form-control" id="image" placeholder="Enter image">
            </div>
            <button type="button" class="btn btn-primary" @click="addProduct">Submit</button>
        </form>
    </div>
</template> 