<script>
	import { writable } from 'svelte/store';
	import Todo from './Todo.svelte';
	
	let title = '';
	let todos = writable([]);
	let id = 0;	// crypto-random-string, uuid 등 외부라이브러리 사용 가능
	
	function createTodo() {
		if (!title.trim()) { title = ''; alert('Empty!'); return }
		$todos.push({ id, title });	// id: id, title: title
		$todos = $todos;	// 반응성
		title = '';
		id += 1;
	}
</script>

<input bind:value={title} type="text"
	on:keydown={(e) => { e.key == 'Enter' && createTodo() }}/>
<!--
	if (e.key === 'Enter') { createTodo() }
	e.key === 'Enter' ? createTodo() : undefined
	e.key === 'Enter' && createTodo()
-->
<button on:click={createTodo}>Create Todo</button>

{#each $todos as todo}
	<Todo {todos} {todo} />
{/each}