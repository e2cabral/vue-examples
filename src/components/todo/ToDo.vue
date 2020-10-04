<template>
  <section class="todo">
    <ul class="todo__list">
      <li class="todo__listItem" v-if="item.id === 0 && item.name === ''">
        <h3>Sem informações para exibir</h3>
      </li>
      <template v-else>
      <li class="todo__listItem" v-for="[key, value] of returnTodos" :key="key">
        <h3>{{ value.name }}</h3>
        <span>
          <strong>
            {{ value.status ? 'Finished' : 'Not Finished' }}
          </strong>
        </span>
        <button @click="toggleDone(value.id)">{{ value.status ? 'Undone' : 'Done' }}</button>
        <button v-if="value.status" @click="remove(value.id)">Remove</button>
      </li>
      </template>
    </ul>
  </section>
</template>

<script lang="ts">
import {
  Vue, Component, ProvideReactive, Watch, Prop,
} from 'vue-property-decorator';

@Component
export default class ToDo extends Vue {
  @Prop() item!: { id: string; name: string; status: boolean };
  @ProvideReactive() todos: Map<string, { id: string; name: string; status: boolean }> = new Map();

  @Watch('item', { immediate: true, deep: true })
  onItemChange() {
    if (this.item !== undefined) {
      this.todos.set(this.item.id, this.item);
    }
  }

  toggleDone(id: string) {
    const item = this.todos.get(id);
    item!.status = !item!.status;
    this.todos.set(id, item!);
  }
  get returnTodos() {
    return this.todos;
  }

  remove(id: string) {
    this.todos.delete(id);
  }
}
</script>

<style scoped>

</style>
