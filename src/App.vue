<template>
  <section>
    <div>
      <input
          v-model='ticker'
          @keydown.enter='add'
          type='text'
          name='wallet'
          placeholder='Например DOGE'
      />
    </div>
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
      ticker: 'default',
      tickers: [],
      sel: null,
    }
  },

  methods: {
    add() {
      const currentTicker = {
        name: this.ticker,
        price: '-',
      }

      this.tickers.push(currentTicker);
      this.ticker = '';
    },

    select(ticker) {
      this.sel = ticker;
    },

    handleDelete(tickerToRemove) {
      this.tickers = this.tickers.filter(t => t !== tickerToRemove);
    }
  }
}
</script>
