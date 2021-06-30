<script>
//import {link} from 'svelte-spa-router'
//import Nav from '../../components/Navi.svelte';
import client from '../../apollo-client'
import { setClient } from "svelte-apollo";
import QGL_TASK from '../../graphql/task';

//
setClient(client);
export let params = Params, item = {}
console.log(params.id)

const  get_item = async function (id){
  var data = await client.query({
    query: QGL_TASK.GET_TASK(id) ,fetchPolicy: "network-only"
  })
  item = data.data.task  
}
console.log(params.id)
get_item(params.id)
async function handleClick() {
//  alert('clicked')
  await save_item()
}
async function handleClickDelete() {
console.log('handleClickDelete')
  await delete_item()
}
async function delete_item(){
  try {
    const result = await client.mutate({
      mutation: QGL_TASK.DELETE_TASK(params.id)
    })
console.log(result)     
    window.location.href = '/#/tasks/'
  } catch (error) {
    console.error(error);
  }
}
async function save_item(){
  try {
    var title = document.getElementById('title');
//console.log(title.value)
    const result = await client.mutate({
      mutation: QGL_TASK.UPDATE_TASK(params.id, title.value)
    })
    console.log(result)     
    window.location.href = '/#/tasks/'
  } catch (error) {
    console.error(error);
  }    
}
</script>

<!-- -->
<div class="container">
	<h3>Tasks - edit</h3>
  ID : {params.id}
  <hr />
  <div class="form-group">
    <label>Title:</label>
    <input type="text" class="form-control" name="title" id="title" 
    value={item.title} />
    <hr />
    <button on:click={handleClick} class="btn btn-primary">Save</button>
    <hr />
    <button on:click={handleClickDelete} class="btn btn-outline-danger">Delete
    </button>
  </div>

  <hr />
</div>
