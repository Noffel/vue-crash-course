<template>
  <div>
      <form @submit="addTodo">
          <input type="text" v-model="title" name="title" placeholder="Add Todo...">
          <input type="submit" value="Submit" class="btn">
        
      </form>
  </div>
</template>



<script>
//import {v4} from 'uuid';


export default {
    name: "AddTodo",
    data() {
        return {
            title: ""
        }
    },

    methods: {
        addTodo(e) {
            e.preventDefault(); //Stops the default behaviour (trying to submit to a file)
            //const uuid = v4()
            const newTodo = {
               // id: uuid,
                title: this.title,
                completed: false
            }

            // Send up to parent 
            this.$emit('add-todo', newTodo);
            // To clear the form after submitting
            this.title = '';

        }

    }
}
</script>
 


<style scoped>
    form{
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 2;
    }


</style>