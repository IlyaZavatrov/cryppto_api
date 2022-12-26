<script >
export default {
  name: "App",

  data() {
    return {
      ticker: "",
      tickers: [
      ],
      sel: null 
    }
  },

  methods: {
    add() {
      const newTicker = {
        name: this.ticker,
        price: "-"
      };
      this.tickers.push(newTicker);
      setInterval (async () => {
        const f = await fetch
        (`https://min-api.cryptocompare.com/data/price/?fsym=${newTicker.name}&tsyms=USD&api_key=00278035b90b67a2a529a14762c2abb0711639725884c9307c6c2a541c703f5b`);
        const data = await f.json();

        this.tickers.find(t => t.name === newTicker.name).price = data.USD;
      }, 3000);
      this.ticker = "";
    },

    handleDelete(tickerToRemove) {
      this.tickers = this.tickers.filter(t => t != tickerToRemove);
    }
  }
}
</script>

<template v-if="tickers.length">
  <div class="max-w-xs">
    <label for="wallet" class="block">
      Тикер
    </label>
  </div>
  <div class="input">
    <input v-model="ticker" v-on:keydown.enter="add" name="wallet" id="wallet" type="text" placeholder="Ввод">
  </div>
  <div class="button">
    <button type="button" class="btn btn-secondary" @click="add">Добавить
    </button>
  </div>
  <div 
    v-for="t in tickers" 
    :key="t.name"
    @click="sel = t"
    :class="{
      'border-4' : sel === t 
    }"
    class="bg-white overflow-hidden shadow rounded-lg border-purple-800 border-solid cursor-pointer"
    >
  <div class="px-4 py-5 sm:p-6 text-center">
      <dt class="text-sm font-medium text-gray-500 truncate">
        {{ t.name }} - USD
      </dt>
      <dd class="mt-1 text-3xl font-semibold text-gray-900">
        {{ t.price }}
      </dd>
    </div>
    <div class="w-full border-t border-gray-200"></div>
    <button @click.stop="handleDelete(t)"
      class="flex items-center justify-center font-medium w-full bg-gray-100 px-4 py-4 sm:px-6 text-md text-gray-500 hover:text-gray-600 hover:bg-gray-200 hover:opacity-20 transition-all focus:outline-none">
      <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="#718096" aria-hidden="true">
        <path fill-rule="evenodd"
          d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
          clip-rule="evenodd"></path>
      </svg>Удалить
    </button>
  </div>

<section v-if="sel" class="relative">
  <h3 class="text-lg leading-6 font-medium text-gray-900 my-8">
    {{sel.name }} - USD
  </h3>
  <div class="flex items-end border-gray-600 border-b border-l h-64">
    <div
      class="bg-purple-800 border w-10 h-24"
    ></div>
    <div
      class="bg-purple-800 border w-10 h-32"
    ></div>
    <div
      class="bg-purple-800 border w-10 h-48"
    ></div>
    <div
      class="bg-purple-800 border w-10 h-16"
    ></div>
  </div>
  <button
    @click="sel = null"
    type="button"
    class="absolute top-0 right-0"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      xmlns:svgjs="http://svgjs.com/svgjs"
      version="1.1"
      width="30"
      height="30"
      x="0"
      y="0"
      viewBox="0 0 511.76 511.76"
      style="enable-background:new 0 0 512 512"
      xml:space="preserve"
    >
      <g>
        <path
          d="M436.896,74.869c-99.84-99.819-262.208-99.819-362.048,0c-99.797,99.819-99.797,262.229,0,362.048    c49.92,49.899,115.477,74.837,181.035,74.837s131.093-24.939,181.013-74.837C536.715,337.099,536.715,174.688,436.896,74.869z     M361.461,331.317c8.341,8.341,8.341,21.824,0,30.165c-4.16,4.16-9.621,6.251-15.083,6.251c-5.461,0-10.923-2.091-15.083-6.251    l-75.413-75.435l-75.392,75.413c-4.181,4.16-9.643,6.251-15.083,6.251c-5.461,0-10.923-2.091-15.083-6.251    c-8.341-8.341-8.341-21.845,0-30.165l75.392-75.413l-75.413-75.413c-8.341-8.341-8.341-21.845,0-30.165    c8.32-8.341,21.824-8.341,30.165,0l75.413,75.413l75.413-75.413c8.341-8.341,21.824-8.341,30.165,0    c8.341,8.32,8.341,21.824,0,30.165l-75.413,75.413L361.461,331.317z"
          fill="#718096"
          data-original="#000000"
        ></path>
      </g>
    </svg>
  </button>
</section>
</template>


<style src="./app.css">

</style>

