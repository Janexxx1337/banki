<template>
  <div class="card">
    <img :src="img" :alt="heading" @click="$emit('view-details', { ...item })" />
    <h2 @click="$emit('view-details', { ...item })">
      {{ heading }}</h2>
<h3>{{author}}</h3>
    <div class="card__buy">
      <p>
        <span class="grey__price">{{ salePrice }}</span>
        <span class="actual__price">{{ actualPrice }}</span>
      </p>
      <button @click="addToCart" :disabled="buttonState === 'inCart'">
        <span v-if="buttonState === 'default'">{{ buttonText }}</span>
        <span v-else-if="buttonState === 'processing'">
            <svg class="spin" width="20" height="20" viewBox="0 0 32 32">
            <circle cx="16" cy="16" r="12" stroke="#fff" stroke-width="3" fill="none" stroke-dasharray="56.548" stroke-dashoffset="56.548"></circle>
          </svg>
        </span>
        <span v-else-if="buttonState === 'inCart'">
          <span class="inCart">
            <svg class="done" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" stroke="#fff" stroke-width="3">
            <path d="M9 16.172l-5.516-5.249-1.484 1.327 7 6.75 12-12-1.484-1.328z"/>
          </svg> В корзине
          </span>
        </span>
      </button>
    </div>
  </div>
</template>


<script>
export default {
  name: "CardModule",
  props: {
    id: Number,
    img: String,
    heading: String,
    author: String,
    salePrice: String,
    actualPrice: String,
    buttonText: String,
    description: String,
    images: Array,
  },
  computed: {
    item() {
      return {
        id: this.id,
        img: this.img,
        heading: this.heading,
        author: this.author,
        salePrice: this.salePrice,
        actualPrice: this.actualPrice,
        buttonText: this.buttonText,
        description: this.description,
        images: this.images,
      };
    },
  },
  data() {
    return {
      buttonState: this.getButtonStateFromLocalStorage(),
    };
  },
  methods: {
    addToCart() {
      if (this.buttonState === "default") {
        this.buttonState = "processing";
        setTimeout(() => {
          this.buttonState = "inCart";
          this.saveButtonStateToLocalStorage();
          this.$emit("addToCart", this.id);
        }, 2000);
      }
    },
    openModal(id) {
      this.selectedItem = this.items.find(item => item.id === id);
      console.log('selectedItem:', this.selectedItem);
      this.isModalVisible = true;
    },

    saveButtonStateToLocalStorage() {
      const cardKey = `card-${this.id}`;
      if (this.buttonState && typeof this.buttonState === "string") {
        localStorage.setItem(cardKey, this.buttonState);
      }
    },

    getButtonStateFromLocalStorage() {
      const cardKey = `card-${this.id}`;
      const state = localStorage.getItem(cardKey);
      return state ? state : "default";
    },

  },
};
</script>






<style scoped>
button.in-cart {
  background-color: #5B3A32;
}

p .grey__price {
  display: block;
  margin-top: 23px;
  margin-bottom: 2px;
  font-weight: 300;
  font-size: 14px;
  line-height: 150%;
  align-items: center;
  text-decoration-line: line-through;
  color: #A0A0A0;
}

.actual__price {
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 150%;
  color: #343030;
}

.card h2 {
  margin-top: 12px;
  max-width: 220px;
  font-weight: 400;
  font-size: 18px;
  line-height: 150%;
  color: #343030;
}

.card__buy {
  display: flex;
  align-items: center;
  gap: 21px;
}

button {
  max-height: 48px;
  max-width: 118px;
  margin-top: 22px;
  text-align: center;
  transition: background-color .2s ease-in;
}

button:hover {
  background-color: #776763;
}

button:disabled {
  background-color: #5B3A32;
}

.purchased {
  display: flex;
}

.spin {
  animation: spin 1s infinite linear;
}

.done {
  color: green;
  width: 20px;
  height: 20px;
}

@keyframes spin {
  from {transform: rotate(0deg);}
  to {transform: rotate(360deg);}
}

.inCart {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 120px;
}

h3 {
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 150%;
  color: #343030;
}

@media (max-width: 1440px) {

  h3 {
    font-size: 16px;
    margin-top: 5px;
    text-align: center;
  }
  h2 {
   margin: 0 auto;
    text-align: center;
  }
  .card__buy {
    display: flex;
    flex-direction: column;
    font-size: 24px;
  }

  button {
    margin: 0;
  }
  .card img {
    display: block;
    margin: 0 auto;
  }
  span.grey__price {
    margin: 0;
  }
}

</style>