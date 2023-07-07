<template>
  <el-container>
    <el-header>
      <el-button class="login-button" type="primary" plain>
        <el-icon class="icon-user" name="el-icon-user"></el-icon>
        登录
      </el-button>
    </el-header>
    <el-main style="padding: 10px;">
      <el-divider class="custom-divider"></el-divider>
      <div class="products-grid">
        <div class="product-card" v-for="product in products" :key="product.id">
          <el-card :body-style="{ padding: '0px' }">
            <div style="padding: 14px;">
              <div class="product-name">{{ product.name }}</div>
              <div class="product-price">{{ product.price }}</div>
            </div>
            <el-image
              fit="cover"
              :src="product.image"
              height="200px"
              width="200px"
              class="product-image"
            />
            <div style="padding: 14px;">
              <el-button type="primary">购买</el-button>
            </div>
          </el-card>
        </div>
      </div>
    </el-main>
  </el-container>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      products: [
        { id: 1, name: '商品1', price: '￥100', image: 'image1.jpg' },
        { id: 2, name: '商品2', price: '￥200', image: 'image2.jpg' },
        { id: 3, name: '商品3', price: '￥300', image: 'image3.jpg' },
        // 添加更多商品...
      ]
    }
  },
  async mounted() {
    try {
      const response = await axios.get('http://127.0.0.1:5000/products');  // 用你的 API 替换这个 URL
      this.products = response.data;  // 假设你的 API 返回的数据在 response.data 中
    } catch (error) {
      console.error('Failed to load products:', error);
    }
  }
}
</script>

<style scoped>
.el-header {
  display: flex;
  justify-content: flex-end;
  padding: 10px;
}

.login-button {
  color: gray;
}

.icon-user {
  font-size: 24px;
}

.custom-divider {
  border-top: 1px solid lightgray;
  margin: 10px 0;
}

.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

.product-card {
  border: 1px solid #eee;
  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
}

.product-name {
  font-size: 16px;
  font-weight: bold;
}

.product-price {
  color: #ff4500;
}

.product-image {
  height: 200px;
  width: 200px;
  object-fit: cover;
}
</style>
