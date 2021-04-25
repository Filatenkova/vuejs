<template class="app">
  <section>
    <div class="app__margin-5">
      <input
          v-model.trim='ticker'
          @keydown.enter='add'
          type='text'
          name='wallet'
          placeholder='Например DOGE'
      />
    </div>
    <template v-if='tickers.length'>
      <div class="app__margin-10">
        <span
            v-for='t in tickers'
            :key='t.name'
            @click="enterToInput(t.name)"
            class="app__prompt"
        >
        {{ t.name }}
      </span>
      </div>
      <div v-if="error">Такой тикер уже добавлен</div>
    </template>
    <button
        @click='add'
        type='button'
    >Добавить
    </button>
  </section>
  <template v-if='tickers.length'>
    <ul>
      <li
      v-for='t in tickers'
      :key='t.name'
      @click="select(t)"
      >
        <span>{{ t.name }}</span>
        &nbsp
        <button
          @click.stop="handleDelete(t)"
          type='button'
        >
          Удалить
        </button>
      </li>
    </ul>
  </template>
  <section v-if='sel'>
    <span>Вы выбрали:</span>
    <h3>{{ sel.name }}</h3>
    <button
        @click='sel = null'
    >Удалить выбранные значения</button>
  </section>
</template>

<script>

export default {
  name: 'App',

  data() {
    return {
      ticker: '',
      tickers: [],
      sel: null,
      error: false,
    }
  },

  created() {
    const tickersData = localStorage.getItem("cryptonomicon-list");

    if (tickersData) {
      this.tickers = JSON.parse(tickersData);
      this.tickers.forEach(ticker => {
        this.subscribeToUpdates();
      });
    }
  },

  methods: {
    subscribeToUpdates() {
      this.ticker = '';
    },

    add() {
      const currentTicker = {
        name: this.ticker,
        price: '-',
      }

      this.tickers.push(currentTicker);

      localStorage.setItem("cryptonomicon-list", JSON.stringify(this.tickers));
      this.subscribeToUpdates();
    },

    select(ticker) {
      this.sel = ticker;
    },

    handleDelete(tickerToRemove) {
      this.tickers = this.tickers.filter(t => t !== tickerToRemove);
    },

    enterToInput(value) {
      this.ticker = value;
    }
  }
}
</script>
<style src="./assets/app.css"></style>