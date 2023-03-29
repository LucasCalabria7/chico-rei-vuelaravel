<template>
  <div>
    <Header />
    <div id="global-filter">
      <img id="filter-icon" src="./assets/filter.png" />

      <div id="input-area">
        <input id="search" placeholder="O que você procura ?" type="text" v-model="searchValue" />
        <select class="input-select" v-model="selectedMensCategory">
          <option value="">Masculinos</option>
          <option value="mens-shirts">Camisetas</option>
          <option value="mens-shoes">Tênis</option>
          <option value="mens-watches">Relógios</option>
          <option value="sunglasses">Óculos</option>
        </select>
        <select class="input-select" v-model="selectedWomensCategory">
          <option value="">Femininos</option>
          <option value="womens-dresses">Vestidos</option>
          <option value="womens-shoes">Sapatos</option>
          <option value="womens-watches">Relógios</option>
          <option value="womens-bags">Bolsas</option>
          <option value="womens-jewellery">Jóias</option>
        </select>
        <select class="input-select" v-model="selectedPriceCategory">
          <option value="">Preço</option>
          <option value="expensives">Maiores Preços</option>
          <option value="cheaps">Menores Preços</option>
        </select>
        <select class="input-select" v-model="selectedRatedCategory">
          <option value="">Popularidade</option>
          <option value="top-rated">Mais Populares</option>
          <option value="less-rated">Menos Populares</option>
        </select>
      </div>
    </div>
    <main id="main-container">
      <Card v-for="(produto, index) in pagedProducts" :key="index" :dados-produto="produto" />
    </main>
    <div id="pagination">
      <button id="previous-page" @click="anterior">Anterior</button>
      <div id="page-numbers">
        <button v-for="pagina in numberOfPages" :key="pagina" :class="{ active: pagina === currentPage }"
          @click="goToPage(pagina)">
          {{ pagina }}
        </button>
      </div>
      <button id="next-page" @click="proxima">Próxima</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import './styles/global.css';
import Header from './components/Header.vue';
import Card from './components/Card.vue';

export default {
  name: 'App',
  components: {
    Header,
    Card,
  },
  data() {
    return {
      produtos: [],
      currentPage: 1,
      itemsPerPage: 15,
      searchValue: '',
      selectedMensCategory: '',
      selectedWomensCategory: '',
      selectedPriceCategory: '',
      selectedRatedCategory: '',
    };
  },
  async mounted() {
    const result = [];

    for (let i = 36; i <= 85; i++) {
      const url = `https://dummyjson.com/products/${i}`;
      const res = await axios.get(url);
      result.push(res.data);
    }

    this.produtos = result;
  },
  computed: {
    pagedProducts() {
      let filteredList = this.produtos;

      // Aplicar filtros

      //Busca
      if (this.searchValue.trim().length > 0) {
        filteredList = filteredList.filter((produto) => {
          return produto.title.toLowerCase().includes(this.searchValue.trim().toLowerCase());
        });
      }
      //Categoria Masculina
      if (this.selectedMensCategory) {
        filteredList = filteredList.filter((produto) => {
          return produto.category.toLowerCase().includes(this.selectedMensCategory.toLowerCase());
        });
      }
      //Categoria Feminina
      if (this.selectedWomensCategory) {
        filteredList = filteredList.filter((produto) => {
          return produto.category.toLowerCase().includes(this.selectedWomensCategory.toLowerCase());
        });
      }
      //Categoria de Preço
      if (this.selectedPriceCategory === "expensives") {
        filteredList = filteredList.sort((a, b) => b.price - a.price);
      } else if (this.selectedPriceCategory === "cheaps") {
        filteredList = filteredList.sort((a, b) => a.price - b.price);
      }
      //Categoria de popularidade
      if (this.selectedRatedCategory === "top-rated") {
        filteredList = filteredList.sort((a, b) => b.rating - a.rating);
      } else if (this.selectedRatedCategory === "less-rated") {
        filteredList = filteredList.sort((a, b) => a.rating - b.rating);
      }

      // Paginar os resultados filtrados
      const initialIndex = (this.currentPage - 1) * this.itemsPerPage;
      const finalIndex = initialIndex + this.itemsPerPage;
      return filteredList.slice(initialIndex, finalIndex);
    },
    numberOfPages() {
      const filteredList = this.productsList;
      return Math.ceil(filteredList.length / this.itemsPerPage);
    },
    productsList() {
      let filteredList = this.produtos;

      // Aplicar filtros
      if (this.searchValue.trim().length > 0) {
        filteredList = filteredList.filter((produto) => {
          return produto.title.toLowerCase().includes(this.searchValue.trim().toLowerCase());
        });
      }

      if (this.selectedMensCategory) {
        filteredList = filteredList.filter((produto) => {
          return produto.category.toLowerCase().includes(this.selectedMensCategory.toLowerCase());
        });
      }

      if (this.selectedWomensCategory) {
        filteredList = filteredList.filter((produto) => {
          return produto.category.toLowerCase().includes(this.selectedWomensCategory.toLowerCase());
        });
      }

      if (this.selectedPriceCategory === "expensives") {
        filteredList = filteredList.sort((a, b) => b.price - a.price);
      } else if (this.selectedPriceCategory === "cheaps") {
        filteredList = filteredList.sort((a, b) => a.price - b.price);
      }

      if (this.selectedRatedCategory === "top-rated") {
        filteredList = filteredList.sort((a, b) => b.rating - a.rating);
      } else if (this.selectedRatedCategory === "less-rated") {
        filteredList = filteredList.sort((a, b) => a.rating - b.rating);
      }

      return filteredList
    }
  },
  methods: {
    anterior() {
      if (this.currentPage > 1) {
        this.currentPage -= 1;
      }
    },
    proxima() {
      if (this.currentPage < this.numberOfPages) {
        this.currentPage += 1;
      }
    },
    goToPage(pageNumber) {
      this.currentPage = pageNumber;
    },
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed&display=swap');

#main-container {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  margin: 1.5rem;
  gap: 1rem;
}

#pagination {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2rem;
}

#previous-page,
#next-page {
  background-color: #db7416;
  color: white;
  border: none;
  border-radius: 100rem;
  width: 5vw;
  height: 5vh;
  cursor: pointer;
}

#page-numbers button {
  background-color: #db7416;
  border: 1px solid white;
  color: white;
  font-size: 1.2rem;
  padding: 0.5rem;
  margin: 0.2rem;
  cursor: pointer;
  border-radius: 100rem;
}

#page-numbers button:hover {
  opacity: 0.9;
}

#page-numbers button.active {
  background-color: #f2efe9;
  color: #fff;
}

#global-filter {
  height: 15vh;
  max-width: 100vw;
  border-bottom: 4px solid #db7416;
  display: flex;
  align-items: center;
  justify-content: center;
}

#filter-icon {
  height: 1.5rem;
  padding: 0 2rem;
}

#input-area {
  display: flex;
  justify-content: space-evenly;
  gap: 1rem;
  width: 75%;
}

#search,
.input-select {
  width: 26vw;
  height: 4vh;
  border-radius: 1rem;
  text-align: center;
}

.input-select {
  width: 12vw;
  font-weight: 600;
  border-radius: 0.5rem;
}
</style>