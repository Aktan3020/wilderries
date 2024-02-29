<template>
  <div class="app">
    <header>
      <nav class="header_top">
        <span><svg width="800px" height="800px" viewBox="-5.07 0 43.012 43.012" class="location_icon"
            xmlns="http://www.w3.org/2000/svg">
            <path id="location"
              d="M406.185,260.012c-18.028-13.493-16.233-28.572-16.233-28.572h11.184a4.7,4.7,0,0,0-.142,1.1,5.378,5.378,0,0,0,.466,2.1,7.353,7.353,0,0,0,2.622,2.615,5,5,0,0,0,4.218,0,7.316,7.316,0,0,0,2.619-2.615,5.4,5.4,0,0,0,.465-2.105,4.728,4.728,0,0,0-.141-1.1h11.5S424.217,246.277,406.185,260.012Zm4.731-29.576a7.353,7.353,0,0,0-2.619-2.618,4.977,4.977,0,0,0-4.211,0,7.389,7.389,0,0,0-2.622,2.618,6.468,6.468,0,0,0-.326,1H389.966c0-7.972,7.335-14.435,16.383-14.435s16.383,6.463,16.383,14.435H411.242A6.523,6.523,0,0,0,410.915,230.436Z"
              transform="translate(-389.902 -217)" />
          </svg> Москва
        </span>
        <span>Продавайте на Wildberries</span>
        <span>Работа в Wildberries</span>
      </nav>
      <div class="header_bottom">
        <h1 class="company_title">
          <img src="https://static-basket-01.wbbasket.ru/vol0/i/v3/header/logo.svg" alt="">
        </h1>
        <div class="burger">
          <div class="burger_wrap">
            <div id="nav-icon4" @click="toggleIcon($event.target)" :class="{ open: !isOpen }">
              <span></span>
              <span></span>
              <span></span>
            </div>
          </div>
        </div>

        <div class="input_wrap">
          <input type="text" placeholder="Найти на Wildberries">
        </div>
        <nav class="header_bottom_nav">
          <span><img src="./assets/icon/location.svg" alt="">Адреса</span>
          <span><img src="./assets/icon/human.svg" alt="">Войти</span>
          <span><img src="./assets/icon/cart.svg" alt="">Корзина</span>
        </nav>
      </div>
    </header>
    <ModalCategory :isOpenModal="isOpenModal" />
  </div>
</template>

<script>
import './assets/css/index.css'
import ModalCategory from './components/ModalCategory.vue';
export default {
  name: 'App',
  data() {
    return {
      isOpen: false,
      isOpenModal: false
    }
  },
  methods: {
    toggleIcon(target) {
      console.log(this.isOpenModal);
      this.isOpen = !this.isOpen;
      this.isOpenModal = !this.isOpenModal;
      target.classList.toggle('open');
    }
  },
  components: {
    ModalCategory
  }
}
</script>

<style></style>
