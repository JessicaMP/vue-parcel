<template>
	<div>
		<nav>
			<input type="checkbox" v-model="selectAll"/>
			<input v-model.trim="val" :placeholder="text" @keyup.enter="saveText"/>
			<button @click="saveText"><i class="fas fa-plus"></i></button>
		</nav>
		<main class="container">
			<ol class="row todo-list">
				<li v-for="(li, index) in filteredTodos" :key="index" class="todo" >
          <div class="view">
            <input type="checkbox" v-model="li.completed" class="toggle">
            <span class="notView editing" @dblclick="editTodo(li)" :class="{completed: li.completed, editing: li === editing}">{{ li.name }}</span>
            <div class="box-buttons">
              <button @click="remove(index)"><i class="fas fa-times"></i></button>
            </div>
          </div>
          <input type="text" class="edit" v-model="li.name" @keyup.enter="doneEdit">
				</li>
			</ol>
		</main>
    <footer class="footer container" v-show="hasTodo">
      <div class="row">
        <span class="todo.count"><strong>{{ remainning }}</strong>Item</span>
        <ul class="filters">
          <li><a :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'" href="t">Todos</a></li>
          <li><a :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'" href="a">Activo</a></li>
          <li><a :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'" href="c">Completo</a></li>
        </ul>
      </div>
    </footer>
	</div>
</template>

<script>
export default {
  data() {
    return {
      val: "",
      text: "Writing....",
      list: [
        { name: "Vue", completed: false },
        { name: "React", completed: false },
        { name: "Angular", completed: false }
      ],
      filter: 'all',
      selectAll: false,
      editing: null
    };
  },
  methods: {
    saveText() {
      if (this.val.length > 0) {
        this.list.push({
          completed: false,
          name: this.val
        });
        this.val = "";
      }
    },
    remove(val) {
      for (let i = 0; i < this.list.length; i++) {
        if (val === i) { 
          this.list.splice(i, 1);
          console.log(val);
        }
      }
    },
    editTodo(li) {
      this.editing = li
    },
    doneEdit() {
      this.editing = null
    }
  },
  computed: {
    remaininig() {
      return this.list.filter(li => !li.completed).length
    },
    filteredTodos() {
      if (this.filter === 'todo') {
        return this.list.filter(li => !li.completed)
      } else if(this.filter === 'done') {
        return this.list.filter(li => li.completed)
      }
      return this.list
    },
    hasTodo() {
      return this.list.length > 0
    }
  },
  watch: {
    selectAll(e) {
      for (let i = 0; i < this.list.length; i++) {
        if (e === true) {
        return this.list.filter(li => li.completed = true)
        } else {
        return this.list.filter(li => li.completed = false)
        return this.remaininig === 0
        }
      }
    }
  }
};
</script>

<style lang="scss" scoped>
nav {
  display: flex;
  justify-content: center;
}

.container {
  display: flex;
  justify-content: center;
}

.row {
  flex-direction: row;
  width: 60%;
  justify-content: center;
}

.box-buttons {
  float: right;
}

ol {
  list-style: none;
  padding: 0;

  li {
    width: 100%;
    border: 0.15rem solid black;
    box-sizing: border-box;
    margin: 0.5rem;
    padding: 0.5rem;
  }

  span {
    display: inline-block;
    text-align: left;
  }
}

.edit {
    margin: 0;
    width: 80%;
    font-family: inherit;
    font-weight: inherit;
    border: 0;
    border: 1px solid #999;
    box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-font-smoothing: antialiased;
    display: none;
}

.todo-list li.editing {
	border-bottom: none;
	padding: 0;
}

.todo-list li.editing .edit {
	display: block;
	width: 506px;
	padding: 13px 17px 12px 17px;
	margin: 0 0 0 43px;
}

.todo-list li.editing .view {
	display: none;
}

.completed {
  color: rgb(65, 184, 131);
  text-decoration: line-through;
}

.footer {
  box-sizing: border-box;
  font-size: 0.9rem;

  span {
    text-align: right;
    padding: 0 1rem;
  }

  .filters {
    float: right;
    list-style: none;
    text-align: left;
    margin: 0;

    li {
      display: inline-block;
      padding: 0 1rem;

      a {
        color: black;
        text-decoration: none;
        padding: 0.2rem;
        
      }
    }
  }
}
.filters li a.selected, .filters li a:hover {
  border: 2px solid rgb(65, 184, 131);
  border-radius: 0.5rem;
}
</style>