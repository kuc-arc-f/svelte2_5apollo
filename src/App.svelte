<script>
import Router from 'svelte-spa-router'
import Nav from './components/Navi.svelte';
import index from './pages/index.svelte'
import about from './pages/about.svelte'

/* tasks */
import tasks from './pages/tasks/index.svelte'
import tasks_create from './pages/tasks/create.svelte'
import tasks_show from './pages/tasks/show.svelte'
import tasks_edit from './pages/tasks/edit.svelte'

export const routes = {
  '/': index,
  '/about': about,  
  /* tasks */
  '/tasks/': tasks,
  '/tasks/create': tasks_create,
  '/tasks/show/:id': tasks_show, 
  '/tasks/edit/:id': tasks_edit, 
   
}
</script>

<main>
  <Nav />
  <Router {routes} />
  <hr />
</main>

<style>
</style>