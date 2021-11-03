<template>
    <form @submit.prevent="onSubmit">
      <div class="d-flex">
        <div class="flex-grow-1 me-2">
          <input type="text" class="form-control" v-model="todo" placeholder="Type new To-Do"/>
        </div>
        <div>
          <button type="submit" class="btn btn-primary">Add</button>
        </div>
      </div>
      <div style="color:red" v-show="hasError">This Field Cannot Be Empty!</div>
    </form>
</template>

<script>
    import {ref} from 'vue';

    export default{
        setup(props, context){
            const todo = ref('');
            const hasError = ref(false);
            
            const onSubmit = () => {
                if(todo.value === ''){
                    hasError.value = true;
                }else{
                    context.emit('add-todo', {
                        id: Date.now(),
                        subject : todo.value,
                        completed : false,
                    });
                    hasError.value = false;
                    todo.value = '';
                }
            }

            return{
                todo,
                hasError,
                onSubmit
            }
        }
    }

</script>

<style>

</style>