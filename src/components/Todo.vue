<template>
  <div id="app">
    <div>
      <h1>Заметки</h1>

      <form>
        <div>
          <label for="text">Задача </label>
          <input type="text" id="text" v-model="text">
        </div>
        <div>
	  <label for="type">Тип </label>
		<select id="type" v-model="type">
  		<option value="Личное">Личное</option>
  		<option value="Мероприятие">Мероприятие</option>
  		<option value="Работа">Работа</option>
  		<option value="Другое">Другое</option>
	  </select>

	</div>

        <div>
          <label>Срочность:</label>
          <div>
            <input type="radio" id="priority-low" value="Не срочно" v-model="priority">
            <label for="priority-low">Не срочно</label>
          </div>
          <div>
            <input type="radio" id="priority-high" value="Срочно" v-model="priority">
            <label for="priority-high">Срочно</label>
          </div>
        </div>

        <button @click="add">Добавить заметку</button>
        <button @click="reset">Сбросить данные</button>
      </form>

<ul>
        <li v-for="note in this.notes">
          <div>
            <p><b>{{ note.text }} </b>: {{ note.type }} ({{ note.priority }}) {{ note.check ? '✔' : ' ' }}<input type="checkbox" v-model="note.check" id="check"></p>
            <div>
              
            </div>
          </div>
        </li>
      </ul>


    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: '',
      type: 'Личное',
      priority: 'Не срочно',
      check: false,
      notes: JSON.parse(localStorage.getItem('notes')) || [],
      
    };
  },

  methods: {
    add() {
      const newNote = {
        text: this.text,
        type: this.type,
        priority: this.priority,
	check: this.check,
      };

      this.notes.push(newNote);
      this.save();
      this.clean();
    },
    save() {
      localStorage.setItem('notes', JSON.stringify(this.notes));
    },
    clean() {
      this.text = '';
      this.type = 'Личное';
      this.priority = 'Не срочно';
      this.check = false;
    },
    reset() {
      localStorage.removeItem('notes');
      this.notes = [];
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
}
ul {
  list-style: none;
}
div, button {
  margin: 10px;
}
</style>