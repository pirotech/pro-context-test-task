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
            <span v-if="card.done" class="_done">Выполнено</span>
            <span v-if="!card.done">Не выполнено</span>
          </p>
          <button class="cards-item__edit" @click="openEditModal(card)">Редактировать</button>
        </li>
        <li class="cards-item cards-item_button">
          <button
            class="cards__create-new"
            @click="openCreateNewModal"
          >Добавить</button>
        </li>
      </ul>
    </div>

    <div v-if="createNew.modal" class="main-page-modal" @click.self.stop="closeCreateNewModal">
      <div class="modal-wrapper">
        <h4>Добавить карточку</h4>
        <UiTextField
          class="modal__name"
          label="Имя"
          :value="createNew.form.name"
          :error="createNew.form.nameError"
          :onChange="e => this.onChangeCreateNewField('name', e.target.value)"
        />
        <div class="modal-buttons">
          <button class="modal__cancel" @click="closeCreateNewModal">Отмена</button>
          <button class="button_primary modal__submit" @click="createNewCard">Создать</button>
        </div>
      </div>
    </div>

    <div v-if="edit.modal" class="main-page-modal" @click.self.stop="closeEditModal">
      <div class="modal-wrapper">
        <h4>Редактировать карточку</h4>
        <UiTextField
          class="modal__name"
          label="Имя"
          :value="edit.form.name"
          :error="edit.form.nameError"
          :onChange="e => this.onChangeEditField('name', e.target.value)"
        />
        <UiCheckbox
          :label="edit.form.done ? 'Выполнено' : 'Не выполнено'"
          :value="edit.form.done"
          :onChange="() => this.onChangeEditField('done', !edit.form.done)"
        />
        <div class="modal-buttons">
          <button class="modal__cancel" @click="closeEditModal">Отмена</button>
          <button class="button_primary modal__submit" @click="editCard">Редактировать</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UiCheckbox from "../components/UiCheckbox";
import UiTextField from "../components/UiTextField";

export default {
  name: 'MainPage',
  components: {
    UiCheckbox,
    UiTextField
  },
  data() {
    return {
      cards: [
        {
          id: 0,
          name: 'Cook sandwich',
          done: true
        }
      ],
      createNew: {
        modal: false,
        form: {
          name: '',
          nameError: ''
        }
      },
      edit: {
        modal: false,
        form: {
          name: '',
          nameError: '',
          done: false,
        }
      }
    };
  },
  methods: {
    openCreateNewModal() {
      this.createNew.modal = true;
    },
    onChangeCreateNewField(name, value) {
      this.createNew.form[name] = value;
      this.createNew.form[name + 'Error'] = '';
    },
    createNewCard() {
      const { name } = this.createNew.form;
      if (!name) {
        this.createNew.form.nameError = 'Обязательное поле';
        return;
      }

      const created = {
        id: Math.round(Math.random() * 1000),
        name,
        done: false
      };
      this.cards.push(created);
      this.closeCreateNewModal();
    },
    closeCreateNewModal() {
      this.createNew.modal = false;
      this.createNew.form.name = '';
      this.createNew.form.nameError = '';
    },

    openEditModal(item) {
      this.edit.modal = true;
      this.edit.form = {
        ...this.edit.form,
        ...item
      }
    },
    onChangeEditField(name, value) {
      this.edit.form[name] = value;
      this.edit.form[name + 'Error'] = '';
    },
    editCard() {
      const { id, name, done } = this.edit.form;
      if (!name) {
        this.edit.form.nameError = 'Обязательное поле';
        return;
      }

      const edited = { id, name, done };
      this.cards = this.cards.map(item => item.id === id ? edited : item);
      this.closeEditModal();
    },
    closeEditModal() {
      this.edit.modal = false;
    }
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
    flex-wrap: wrap;
    .cards {
      display: flex;
      &-item {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        min-width: 300px;
        max-width: 300px;
        padding: 20px;
        margin-right: 20px;
        margin-bottom: 20px;
        background-color: white;
        border-radius: 2px;
        &_button {
          align-items: center;
        }
        &__name {
          width: 100%;
          text-align: left;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }
        &__status {
          margin-top: 12px;
          ._done {
            color: #228c22;
          }
        }
        &__edit {
          margin-top: 12px;
        }
      }
      &__create-new {
      }
    }
  }
  &-modal {
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    min-height: 100vh;
    background-color: rgba(0, 0, 0, .6);
    .modal {
      &-wrapper {
        width: 100%;
        max-width: 500px;
        padding: 20px;
        background-color: white;
        border-radius: 2px;
      }
      &__name {
        margin-top: 12px;
      }
      &-buttons {
        display: flex;
        justify-content: flex-end;
        margin-top: 12px;
      }
      &__cancel {}
      &__submit {
        margin-left: 8px;
      }
    }
  }
}
</style>
