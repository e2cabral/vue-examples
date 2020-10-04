<template>
  <section>
    <form class="input__todo">
      <label>
        <input type="text" placeholder="Type a task name..." v-model="name" />
      </label>
      <label for="status-ok" class="status-check">
        <span>
          <input id="status-ok" type="radio" name="status" :value="true" v-model="status">
          Finished
        </span>
        <span>
          <input id="status-not-ok" type="radio" name="status" :value="false" v-model="status">
          Not Finished
        </span>
      </label>
      <label for="btn">
        <button id="btn" @click.prevent="add({name, status})">
          Add
        </button>
      </label>
    </form>
  </section>
</template>

<script lang="ts">
import {
  Vue, Component, Emit, ProvideReactive,
} from 'vue-property-decorator';

@Component
export default class CreateToDo extends Vue {
  index = 0;
  todos!: { id: number; name: string; status: boolean };

  @ProvideReactive() name = '';
  @ProvideReactive() status = false;

  @Emit('returnTodo')
  emitTodos() {
    return this.todos;
  }

  add(todo: { name: string; status: boolean }) {
    // eslint-disable-next-line no-plusplus
    this.todos = { id: this.index++, ...todo };
    this.emitTodos();
  }
}
</script>

<style scoped>

</style>
