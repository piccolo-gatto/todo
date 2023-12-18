<template>
  <div id="app">
    <div  class="card p-5">
      <h1>Новая заметка</h1>

      <form>
		<div class="row">
        		<div class="col mb-3">
          			<label for="text" class="form-label">Задача </label>
          			<input type="text" id="text" v-model="text" class="form-control">
        		</div>
        		<div class="col mb-3">
	  			<label for="type" class="form-label">Тип </label>
				<select id="type" v-model="type"  class="form-control">
  					<option value="Личное">Личное</option>
  					<option value="Мероприятие">Мероприятие</option>
  					<option value="Работа">Работа</option>
  					<option value="Другое">Другое</option>
	  			</select>
			</div>
		</div>
        	<div>
			<label class="form-label">Срочность:</label>
			<div class="form-check form-check-inline">
            			<input type="radio" id="priority-low" value="Не срочно" v-model="priority"  class="form-check-input" >
            			<label for="priority-low" class="form-label">Не срочно</label>
			</div>
			<div  class="form-check form-check-inline">
				<input type="radio" id="priority-high" value="Срочно" v-model="priority"  class="form-check-input" >
				<label for="priority-high" class="form-label">Срочно</label>
			</div>
        	</div>
		<div class="row">
        		<div class="col mb-3">
        			<button @click="add" class="btn btn-primary">Добавить заметку</button>
        		</div>
        		<div class="col mb-3">
        			<button @click="reset" class="btn btn-primary">Сбросить данные</button>
  			</div>
  		</div>
      </form>
</div>
<h1>Мои заметки</h1>
<div class="card p-5">
	<ul>
        	<li v-for="note in this.notes">
          		<div>
            			<p><b>{{ note.text }} </b>: {{ note.type }} ({{ note.priority }}) {{ note.check ? '✔' : ' ' }}<input type="checkbox" v-model="note.check" id="check"  class="form-check-input" ></p>
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
  text-align: center;
}
ul {
  list-style: none;
}
div, button {
margin: 5px;
}
</style>