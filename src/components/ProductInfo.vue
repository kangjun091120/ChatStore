<template>
    <el-card class="box-card">
        <div slot="header" class="clearfix">
            <span>{{ product.name }}</span>
        </div>
        <div v-for="(item, index) in product.details" :key="index">
            <span>{{ item.title }}: </span>
            <span>{{ item.content }}</span>
        </div>
        <div>
            <span>Price: {{ product.price }}</span>
        </div>
        <div>
            <img :src="product.image" alt="Product Image">
        </div>
        <div>
            <el-button type="primary">Add to Cart</el-button>
        </div>
    </el-card>
</template>
  
<script>
export default {
    data() {
        return {
            product: {
                name: 'Product Name',
                price: '100',
                image: 'https://example.com/image.jpg',
                details: [
                    {
                        title: 'Description',
                        content: 'This is a wonderful product.',
                    },
                    {
                        title: 'Specifications',
                        content: 'These are the specifications.',
                    },
                ],
            },
        };
    },
};
</script>
  
<style scoped>
.el-card {
    width: 300px;
    margin: 20px auto;
}
</style>
  