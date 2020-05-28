<template>
  <div class="main-page">
    <h1>Карточки</h1>
    <div class="main-page-content">
      <ul v-if="cards" class="main-page-cards">
        <li
          v-for="card in cards"
          :key="card.id"
          class="cards-item"
        >
          <h4 class="cards-item__name">{{card.name}}</h4>
          <p class="cards-item__status">
            <strong>Статус: </strong>
            <span v-if="card.done" class="card-item__status_done">Выполнено</span>
            <span v-if="!card.done">Не выполнено</span>
          </p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainPage',
  data() {
    return {
      cards: [
        {
          id: 0,
          name: 'Cook sandwich',
          done: false
        }
      ]
    };
  }
}
</script>

<style lang="scss">
.main-page {
  display: flex;
  flex-direction: column;
  justify-content: stretch;
  width: 100%;
  min-height: 100vh;
  background-color: #f5f5f5;
  h1 {
    padding: 20px 0;
    background-color: white;
  }
  &-content {
    padding: 20px;
  }
  &-cards {
    display: flex;
    .cards {
      display: flex;
      &-item {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        padding: 20px;
        margin-left: 20px;
        background-color: white;
        border-radius: 2px;
        &:first-child {
          margin-left: 0;
        }
      }
    }
  }
}
</style>
