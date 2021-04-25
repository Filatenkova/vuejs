<template xmlns="http://www.w3.org/1999/html">
  <section>
    <div>
      <input
          type="text"
          name="wallet"
          placeholder="Например DOGE"
      />
    </div>
    <button
        type="button"
    >Добавить
    </button>
  </section>
  <section>
    <ul>
      <li>
        <span>Название валюты</span>
        <span>: </span>
        <span>Цена</span>
        &nbsp
        <button
         type="button"
        >
          Удалить
        </button>
      </li>
    </ul>
  </section>
</template>

<script>

export default {
  name: 'App',
}
</script>
