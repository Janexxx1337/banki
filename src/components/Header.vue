<template>
  <header>
    <Navigation :color="'#343030'"/>
    <div class="header__navigation">
      <input
          type="text"
          placeholder="Поиск по названию картины"
          v-model="searchValue"
          @input="changeInputColor"
          class="search-input"
      />
      <button type="submit">Найти</button>
    </div>
  </header>
  <section>
    <h1>Картины эпохи возрождения</h1>
    <div class="card-variants">
      <Card
          v-for="item in filteredItems"
          :key="item.id"
          :img="item.img"
          :heading="item.heading"
          :author="item.author"
          :salePrice="item.salePrice"
          :actualPrice="item.actualPrice"
          :buttonText="item.buttonText"
          :id="item.id"
          :inCart="item.inCart"
          @update-cart="updateCartState"
          @view-details="openModal"
          class="card"
      />
      <ProductModal
          :item="selectedItem"
          :open="isModalVisible"
          @close-modal="closeModal"
      />

    </div>
  </section>
</template>

<script>
import Navigation from "@/components/Navigation";
import Card from "@/components/Card";
import {ref, computed} from 'vue';
import ProductModal from "@/components/ProductModal";


export default {
  name: 'HelloWorld',
  components: {Navigation, Card, ProductModal},
  setup() {

    const selectedItem = ref(null);
    const isModalVisible = ref(false);

    const openModal = (item) => {
      selectedItem.value = item;
      isModalVisible.value = true;
    };

    const closeModal = () => {
      selectedItem.value = null;
      isModalVisible.value = false;
    };


    const searchValue = ref('');
    const items = ref([
      {
        id: 1,
        img: process.env.BASE_URL + 'assets/1.png',
        heading: '«Рождение Венеры»',
        author: 'Сандро Боттичелли',
        description: '',
        salePrice: '2 000 000 $',
        actualPrice: '1 000 000 $',
        buttonText: 'Купить',
        inCart: false,
      },
      {
        id: 2,
        img: process.env.BASE_URL + 'assets/2.png',
        heading: '«Тайная вечеря» ',
        author: 'Леонардо да Винчи',
        description: '',
        actualPrice: '3 000 000 $',
        buttonText: 'Купить',
        inCart: false,
      },
      {
        id: 3,
        img: process.env.BASE_URL + 'assets/3.png',
        heading: '«Сотворение Адама» ',
        author: 'Микеланджело',
        description: '«Сотворение Адама» Микеланджело...',
        salePrice: '6 000 000 $',
        actualPrice: '5 000 000 $',
        buttonText: 'Купить',
        inCart: false,
      },
      {
        id: 4,
        img: process.env.BASE_URL + 'assets/4.png',
        heading: '«Урок анатомии»  ',
        author: 'Рембрандт',
        description: '«Сотворение Адама» Микеланджело...',
        actualPrice: 'Продана на аукционе',
        buttonText: 'Купить',
        inCart: false,
      }
    ]);


    const changeInputColor = (event) => {
      if (event.target.value.trim().length > 0) {
        event.target.classList.add('changed');
      } else {
        event.target.classList.remove('changed');
      }
    };


    const filteredItems = computed(() => {
      if (!items.value) {
        return [];
      }
      return items.value.filter((item) =>
          item.heading.toLowerCase().includes(searchValue.value.toLowerCase())
      );
    });

    const getButtonState = (id) => {
      const cardKey = `card-${id}`;
      const cardState = localStorage.getItem(cardKey);
      return cardState === "inCart";
    };

    const updateCartState = (id) => {
      const cardKey = `card-${id}`;
      const cardState = localStorage.getItem(cardKey);

      if (cardState === "inCart") {
        localStorage.setItem(cardKey, "notInCart");
      } else {
        localStorage.setItem(cardKey, "inCart");
      }

      const itemToUpdate = items.value.find((item) => item.id === id);
      if (itemToUpdate) {
        itemToUpdate.inCart = !itemToUpdate.inCart;
      }
    };

    return {
      searchValue,
      changeInputColor,
      filteredItems,
      getButtonState,
      updateCartState,
      selectedItem,
      isModalVisible,
      openModal,
      closeModal,
    };
  },
};


</script>

<style scoped>

header {
  display: flex;
}

.card-variants, h1 {
  display: flex;
  gap: 32px;
  margin: 45px 352px 0 352px;
}

.container {
  display: flex;
  gap: 48px;
  margin: 37px 162px 0 448px;
}

.header__navigation {
  margin: 24px 0;
  display: flex;
  width: 100%;
}

.header__navigation input {
  border: 1px solid #E1E1E1;
  padding: 13px 60px 14px 16px;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 150%;
  text-align: center;
  color: #9F9F9F;
  width: 40%;
}

.header__navigation input::placeholder {
  color: #555555;
}

.header__navigation input.search-input.changed {
  color: #343030;
}

header {
  border-bottom: 1px solid #E1E1E1;
  width: 100%;
}

@media (max-width: 1440px) {
  .container {
    display: flex;
    gap: 48px;
    margin: 37px 28px 0 38px;
  }

  .header__navigation input {
    width: 100%;
  }

  .card-variants {
    flex-wrap: wrap;
    justify-content: space-around;
    width: 70%;
    margin: 0 auto;
  }

  h1 {
    margin: 0;
  }

  .card {
    max-height: 300px;
   margin: 30px 0;

  }

  header {
    flex-wrap: wrap;
  }

  .header__navigation {
    flex-direction: column;
  }

  .header__navigation button {
    display: block;
    width: 50%;
    margin: 10px auto;
  }
}

@media (max-width: 1024px) {
  .header__navigation input {
    width: 100%;
    margin-top: 20px;
  }

  .container {
    margin-left: 15%;
  }

  .card-variants {
    width: 100%;
  }

  .card {
    margin-top: 20px;
  }

  .card-variants, h1 {
    margin: 0;
  }

  h1 {
    margin-top: 20px;
  }
}

@media (max-width: 425px) {
  .container {
    margin-left: 5%;
    font-size: 12px;
    flex-direction: column;
  }

  h1 {
    display: none;
  }

  .header__navigation {
    margin: 0 auto;
  }

  .header__navigation input {
    width: 100%;
  }
}

@media (max-width: 330px) {
  .header__navigation {
    margin: 0 auto;
    flex-direction: column;
  }

  .header__navigation input {
    width: 100%;
    margin-top: 12px;
  }
}
</style>

