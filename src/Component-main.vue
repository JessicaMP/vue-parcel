<template>
	<div>
		<nav>
			<input type="checkbox" v-model="test"/>
			<input v-model.trim="val" :placeholder="text" @keyup.enter="saveText"/>
			<button @click="saveText"><i class="fas fa-plus"></i></button>
		</nav>
		<div class="container">
			<ol>
				<li v-for="(li, index) in list" :key="index">
					<input type="checkbox" name="" id="">
					<span>{{ li }}</span>
					<div class="box-buttons">
						<button @click="remove(li)"><i class="fas fa-times"></i></button>
						<button @click="edit(li)"><i class="fas fa-pencil-alt"  aria-hidden="true"></i></button>
					</div>
				</li>
			</ol>
		</div>
	</div>
</template>

<script>
export default {
  data() {
    return {
      val: "",
      text: "Writing....",
      list: ["Vue", "React", "Angular"]
    };
  },
  methods: {
    saveText() {
				if (this.val.length > 0) {
					this.list.push(this.val);
					this.val = "";
					console.log("ok");
				}
    },

    remove(li) {
      for (let i = 0; i < this.list.length; i++) {
        if (li === this.list[i]) {
          this.list.splice(i, 1);
          console.log("remove");
        }
      }
		},
		
		test() {
			console.log('check');
			
		},

    edit(li) {
      alert("vue");
    }
  },

  updated() {
    console.log(this.title);
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

ol {
  list-style: none;
	padding: 0;
	flex-direction: row;
	width: 60%;
	justify-content: center;
}

.box-buttons {
	// display: inline-block;
	float: right;
}

ol {

	li { 
		width: 100%;
		border: 0.15rem solid black;
		box-sizing: border-box;
		margin: 0.5rem;
		padding: 0.5rem;
	}

	span {
		display: inline-block;
		text-align: left	
	}
}
</style>