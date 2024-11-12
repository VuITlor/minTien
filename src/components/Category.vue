<script setup>
import { reactive, ref, onMounted } from 'vue';
import Axios from 'axios';

onMounted( async() => {
    try {
        const response = await Axios.get('https://6721038098bbb4d93ca71a61.mockapi.io/v2/products');
        console.log(response.data);
    } catch (error) {
        console.log(error);
    }
    
})
const products = reactive([ 
    {
        id: 1,
        name: "Sản phẩm 1",
        description: "Mô tả sản phẩm 1, rất chất lượng và đáng mua.",
        price: 500000,
        image: "http://picsum.photos/id/1/300/300",
    },
    {
        id: 2,
        name: "Sản phẩm 2",
        description: "Mô tả sản phẩm 2, chất lượng tốt và giá phải chăng.",
        price: 300000,
        image: "http://picsum.photos/id/2/300/300",
    },
    {
        id: 3,
        name: "Sản phẩm 3",
        description: "Mô tả sản phẩm 3, sản phẩm cao cấp và nhiều tính năng.",
        price: 1000000,
        image: "http://picsum.photos/id/3/300/300",
    }
]);

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
            <tr>
                <td>1</td>
                <td>Sản phẩm 1</td>
                <td>Mô tả sản phẩm 1, rất chất lượng và đáng mua.</td>
                <td>500000</td>
                <td><img src="http://picsum.photos/id/1/300/300" alt="" style="width: 100px; height: 100px;"></td>
            </tr>
            <tr>
                <td>2</td>
                <td>Sản phẩm 2</td>
                <td>Mô tả sản phẩm 2, chất lượng tốt và giá phải chăng.</td>
                <td>300000</td>
                <td><img src="http://picsum.photos/id/2/300/300" alt="" style="width: 100px; height: 100px;"></td>
            </tr>
            <tr>
                <td>3</td>
                <td>Sản phẩm 3</td>
                <td>Mô tả sản phẩm 3, sản phẩm cao cấp và nhiều tính năng.</td>
                <td>1000000</td>
                <td><img src="http://picsum.photos/id/3/300/300" alt="" style="width: 100px; height: 100px;"></td>
            </tr>
        </tbody>
    </table>
    <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Home 1</a></li>
        <li><a href="#">Home 2</a></li>
        <li><a href="#">Home 3</a></li>
    </ul>
</template>