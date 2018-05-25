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
            <input type="text" class="edit" v-if='li === editing' v-model="li.name" @keyup.enter="doneEdit(li)" @blur="doneEdit(li)">
            <label for="checkbox" class="notView editing" @dblclick="editTodo(li)" :class="{completed: li.completed}">{{ li.name }}</label>
            <div class="box-buttons">
              <button @click="remove(index)"><i class="fas fa-times"></i></button>
            </div>
          </div>
				</li>
			</ol>
		</main>
    <footer class="footer container">
      <div class="row">
        <span v-if="incomplete"><strong>{{ incomplete }}</strong>Item</span>
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
      props: {
        list: {default: []}
      },
      val: "",
      text: "Writing....",
      list: [
        { name: "Vue", completed: false },
        { name: "React", completed: false },
        { name: "Angular", completed: false }
      ],
      filter: 'all',
      selectAll: false,
      editing: {}
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
    doneEdit(li) {
      this.editing = {};
      if (li.name.trim() === '') {
        this.remove(li)
      }
    },
    inProgress(li) {
      return ! li.completed;
    }
  },
  computed: {
    incomplete() {
      return this.list.filter(this.inProgress).length;
    },
    filteredTodos() {
      if (this.filter === 'todo') {
        return this.list.filter(li => !li.completed)
      } else if(this.filter === 'done') {
        return this.list.filter(li => li.completed)
      }
      return this.list
    }
  },
  watch: {
    selectAll(e) {
      for (let i = 0; i < this.list.length; i++) {
        if (e === true) {
        return this.list.filter(li => li.completed = true)
        } else {
        return this.list.filter(li => li.completed = false)
        return this.incomplete === 0
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

  label {
    padding-right: 10px;
    width: 70%;
    font-size: 18px;
    line-height: 24px;
    color: black;
    z-index: 2;
    overflow: hidden;
  }
}

.list li.done label {
	color: #d9d9d9;
	text-decoration: line-through;
}

.edit {
  border: 1px solid #dedede;
	padding-left: 10px;
	width: 70%;
	height: 35px;
	color: #555;
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
    padding: 0;
    box-sizing: border-box;

    li {
      display: inline-block;
      padding: 0 0.8rem;

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

@media only screen and(max-width: 500px) {
  .row {
    width: 80%;
  }

  .edit {
    width: 50%;
  }
  
  .footer {
    font-size: 0.8rem;

    .filters {
      li {
        padding: 0 5px;
      }
    } 
  }
}
</style>