<template>
  <div class="container">
    <div>
      <Navbar />
    </div>
    <section class="main">
      <CreateToDo @returnTodo="teste($event)" />
    </section>
    <main class="main">
      <ToDo :item="todos" />
    </main>
  </div>
</template>

<script lang="ts">
import { Component, Provide, Vue } from 'vue-property-decorator';
import Navbar from '../components/navbar/Navbar.vue';
import ToDo from '../components/todo/ToDo.vue';
import CreateToDo from '../components/todo/CreateToDo.vue';

@Component({
  components: {
    Navbar,
    CreateToDo,
    ToDo,
  },
})
export default class Home extends Vue {
  @Provide() todos: { id: number; name: string; status: boolean } = { id: 0, name: '', status: false };

  teste(item: { id: number; name: string; status: boolean }) {
    this.todos = item;
  }
}
</script>
