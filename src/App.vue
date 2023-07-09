<template>
  <el-container>
    <el-header>
      <el-button class="login-button" round @click="dialogLogin = true">
        <el-icon class="icon-user">
          <User />
        </el-icon>
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
            <el-image fit="cover" :src="product.image" height="200px" width="200px" class="product-image" />
            <div style="padding: 14px;">
              <el-button type="primary" @click="dialogBuy = true">购买</el-button>
            </div>
          </el-card>
        </div>
      </div>
    </el-main>
  </el-container>
  <el-dialog v-model="dialogLogin" title="Shipping address">
    <Login />
  </el-dialog>
  <el-dialog v-model="dialogBuy" title="Shiping address">
    <ProductInfo />
  </el-dialog>
</template>

<script>
import axios from 'axios';
import Login from '@/components/Login.vue'
import ProductInfo from '@/components/ProductInfo.vue'

export default {
  components: {
    Login, ProductInfo
  },
  data() {
    return {
      dialogLogin: false,
      dialogBuy: false,
      products: []
    }
  },
  async mounted() {
    try {
      const response = await axios.get('http://127.0.0.1:5000/products');
      this.products = response.data;
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
  font-size: 18px;
  height: 110%;
  width: 110px;
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
  margin-left: calc((100% - 200px) / 2);
  object-fit: cover;
}
</style>
