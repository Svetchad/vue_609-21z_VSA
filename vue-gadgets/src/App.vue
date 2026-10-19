<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import ProductList from "./components/ProductList.vue";

// Создаем пустой массив
const items = ref([]);

// Функция для загрузки данных с Mokky.dev
const fetchItems = async () => {
  try {
    const { data } = await axios.get(
      "https://003755c8a74ecdc7.mokky.dev/items" // Ваша ссылка
    );
    
    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
    }));
  } catch (e) {
    console.log(e);
  }
};

// Вызываем загрузку при старте
onMounted(async () => {
  await fetchItems();
});
</script>

<template>
  <body class="flex flex-col justify-between h-dvh">
    <div class="mx-auto w-[1440px] mb-25">
      <nav class="py-3 border-b border-b-slate-200">
        <div class="flex items-center justify-between">
          <div class="flex items-center gap-3">
            <img src="/logo.svg" alt="logo" />
            <p class="text-sm">Лучшие цены <br /> в интернет-магазинах</p>
          </div>
          <ul class="flex gap-10">
            <li>
              <a href="" class="flex gap-3 items-center">
                <span class="p-3.5 rounded-xl bg-slate-100 hover:bg-slate-200 transition">
                  <img src="/cart-icon.svg" alt="cart" />
                </span>
                Корзина
              </a>
            </li>
            <li>
              <a href="" class="flex gap-3 items-center">
                <span class="p-3.5 rounded-xl bg-slate-100 hover:bg-slate-200 transition">
                  <img src="/like-outline.svg" alt="like" />
                </span>
                Избранное
              </a>
            </li>
            <li>
              <a href="" class="flex gap-3 items-center">
                <span class="p-3.5 rounded-xl bg-slate-100 hover:bg-slate-200 transition">
                  <img src="/orders-icon.svg" alt="orders" />
                </span>
                Заказы
              </a>
            </li>
          </ul>
        </div>
      </nav>
      
      <main class="pt-10">
        <h1 class="text-[40px] font-bold mb-5">Каталог</h1>
        <!-- Передаем массив items в наш компонент -->
        <product-list :items="items"></product-list>
      </main>
      
    </div>
    <footer class="p-6 bg-slate-100">
      <div class="text-center text-slate-500">
        Copyright © 2026 Behoof, Inc. Все права защищены
      </div>
    </footer>
  </body>
</template>