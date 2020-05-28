<template>
  <div class="main-page">
    <Header
      :onCreateTask="openCreateTaskModal"
      :onCreateGroup="openCreateGroupModal"
    />
    <div class="main-page-content">
      <ul v-if="cards" class="main-page-cards">
        <li v-for="task in tasks" :key="task.id">
          <UiCard
            :value="task"
            :onEdit="openEditModal"
            :onRemove="removeTask"
          />
        </li>
      </ul>
    </div>

    <Modal :opened="createTaskModal.modal" title="Создать карточку" :closeModal="closeCreateTaskModal">
      <UiTextField
        class="create-task-modal__name"
        label="Имя"
        :value="createTaskModal.form.name"
        :error="createTaskModal.form.nameError"
        :onChange="e => this.onChangeCreateTaskField('name', e.target.value)"
      />
      <UiRadioButton
        v-for="(group, index) in groups"
        :key="group.id"
        class="create-task-modal__group"
        name="groupId"
        :label="group.name"
        :value="group.id"
        :checked="index === 0"
        :onChange="onChangeCreateTaskField"
      />
      <div class="create-task-modal-buttons">
        <button class="create-task-modal__cancel" @click="closeCreateTaskModal">Отмена</button>
        <button class="button_primary create-task-modal__submit" @click="createTask">Создать</button>
      </div>
    </Modal>

    <Modal :opened="editTaskModal.modal" title="Редактировать карточку" :closeModal="closeEditTaskModal">
      <UiTextField
        class="edit-task-modal__name"
        label="Имя"
        :value="editTaskModal.form.name"
        :error="editTaskModal.form.nameError"
        :onChange="e => this.onChangeEditTaskField('name', e.target.value)"
      />
      <UiRadioButton
        v-for="group in groups"
        :key="group.id"
        class="create-task-modal__group"
        name="groupId"
        :label="group.name"
        :value="group.id"
        :checked="group.id === editTaskModal.form.groupId"
        :onChange="onChangeEditTaskField"
      />
      <UiCheckbox
        class="edit-task-modal__status"
        :label="editTaskModal.form.done ? 'Выполнено' : 'Не выполнено'"
        :value="editTaskModal.form.done"
        :onChange="() => this.onChangeEditTaskField('done', !editTaskModal.form.done)"
      />
      <div class="edit-task-modal-buttons">
        <button class="edit-task-modal__cancel" @click="closeEditTaskModal">Отмена</button>
        <button class="button_primary edit-task-modal__submit" @click="editCard">Редактировать</button>
      </div>
    </Modal>
  </div>
</template>

<script>
import Header from "../components/Header";
import UiCard from "../components/UiCard";
import Modal from "../components/Modal";
import UiCheckbox from "../components/UiCheckbox";
import UiTextField from "../components/UiTextField";
import UiRadioButton from "../components/UiRadioButton";

export default {
  name: 'MainPage',
  components: {
    Header,
    UiCard,
    Modal,
    UiCheckbox,
    UiTextField,
    UiRadioButton
  },
  data() {
    return {
      cards: [
      ],
      groups: [
        {
          id: 0,
          name: 'Без группы',
          tasks: [
            {
              id: 0,
              name: 'Приготовить ужин',
              done: false
            }
          ]
        },
        {
          id: 1,
          name: 'Срочные',
          tasks: [
            {
              id: 1,
              name: 'Погладить рубашку',
              done: false
            }
          ]
        }
      ],
      searchString: '',
      createTaskModal: {
        modal: false,
        form: {
          name: '',
          nameError: '',
          groupId: 0
        }
      },
      editTaskModal: {
        modal: false,
        form: {
          name: '',
          nameError: '',
          done: false,
          groupId: 0
        }
      }
    };
  },
  computed: {
    tasks() {
      const tasks = this.groups.reduce((sum, group) => {
        const grouped = group.tasks.map(task => {
          const { id, name } = group;
          return {
            ...task,
            group: {id, name}
          };
        });

        let searched = grouped;
        if (this.searchString) {
          searched = grouped.filter(item => (
            item.name.toLowerCase().includes(this.searchString)
          ));
        }

        return [...sum, ...searched];
      }, []);
      return tasks;
    }
  },
  methods: {
    openCreateTaskModal() {
      this.createTaskModal.modal = true;
    },
    onChangeCreateTaskField(name, value) {
      this.createTaskModal.form[name] = value;
      this.createTaskModal.form[name + 'Error'] = '';
    },
    createTask() {
      const { name, groupId } = this.createTaskModal.form;
      if (!name) {
        this.createTaskModal.form.nameError = 'Обязательное поле';
        return;
      }

      const created = {
        id: Math.round(Math.random() * 1000),
        name,
        done: false
      };
      this.groups = this.groups.map(group => {
        if (group.id === groupId) {
          return {...group, tasks: [...group.tasks, created]};
        }
        return group;
      });
      this.closeCreateTaskModal();
    },
    closeCreateTaskModal() {
      this.createTaskModal.modal = false;
      this.createTaskModal.form.name = '';
      this.createTaskModal.form.nameError = '';
    },

    openEditModal(item) {
      this.editTaskModal.modal = true;
      this.editTaskModal.form = {
        ...this.editTaskModal.form,
        ...item,
        groupId: item.group.id
      }
    },
    onChangeEditTaskField(name, value) {
      this.editTaskModal.form[name] = value;
      this.editTaskModal.form[name + 'Error'] = '';
    },
    editCard() {
      const { id, name, done, groupId } = this.editTaskModal.form;
      if (!name) {
        this.editTaskModal.form.nameError = 'Обязательное поле';
        return;
      }

      const edited = { id, name, done };
      // remove old task
      let preparedGroups = this.groups.map(group => {
        const tasks = group.tasks.filter(task => task.id !== id);
        return {...group, tasks};
      });
      // add new task
      preparedGroups = preparedGroups.map(group => {
        if (group.id === groupId) {
          return {...group, tasks: [...group.tasks, edited]};
        }
        return group;
      });
      this.groups = preparedGroups;
      this.closeEditTaskModal();
    },
    closeEditTaskModal() {
      this.editTaskModal.modal = false;
    },

    removeTask(removed) {
      this.groups = this.groups.map(group => {
        const tasks = group.tasks.filter(task => task.id !== removed.id);
        return {...group, tasks};
      });
    },

    openCreateGroupModal() {}
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
  &-content {
    padding: 20px;
  }
  &-cards {
    display: flex;
    flex-wrap: wrap;
  }
  .create-task-modal, .edit-task-modal {
    &__name, &__group {
      margin-top: 12px;
    }
    &__status {
      margin-top: 24px;
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
</style>
