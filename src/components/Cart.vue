<template>
  <div class="col-md-4">
    <h2 class="mb-3">購物車</h2>

    <div v-if="carts.length === 0">購物車是空的</div>
    <ul v-else class="list-group mb-3">
      <li
        v-for="item in carts"
        :key="item.id"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <div>
          <h6 class="my-0">{{ item.name }}</h6>
          <small class="text-muted">數量： {{ item.quantity }}</small>
        </div>
        <div>
          <span class="text-muted">$ {{ item.quantity * item.price }}</span>
          <button class="btn btn-sm btn-outline-danger ms-2" @click="handleRemoveCart(item)">移除</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, inject } from 'vue';
const props = defineProps({
  carts: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['remove-cart']);
const showNotification = inject('showNotification');

const handleRemoveCart = (item) => {
  emit('remove-cart', item);
  showNotification(`已移除一項 ${item.name}`, 'danger');
};
</script>
