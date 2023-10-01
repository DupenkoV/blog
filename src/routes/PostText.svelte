<script>
	export let post;
	export let id;
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	let editingPost = false;
	let prevPost = post;

	// Функция для изменения статуса редактирования поста, а также, в случае внесения изменения,
	// диспатчит событие и текст изменений в "стор".
	function changeEditStatus(payload) {
		editingPost = !editingPost;
		if (payload === 'close') {
			post = prevPost;
		} else if (payload === 'apply') {
			prevPost = post;
			dispatch('edit', { id, post });
		}
	}
</script>

<!-- Компонент отвечается за рэндэр текста поста. Вынес в отдельный компонент, чтобы не перегружать карточку поста -->
{#if editingPost}
	<textarea
		name="post"
		placeholder="Введите сообщение"
		required
		autocomplete="off"
		bind:value={post}
	/>
	<br />
	<div>
		<button title="Сохранить изменения" on:click={() => changeEditStatus('apply')}>&#9989</button>
		<button title="Отменить изменения" on:click={() => changeEditStatus('close')}>&#10060</button>
	</div>
{:else}
	<p>{post}</p>
	<button title="Редактировать" on:click={changeEditStatus}>&#9997;</button>
{/if}

<style>
	textarea {
		width: 90%;
		height: 10rem;
		padding: 1rem;
		margin: 0.7rem;
	}
	div {
		text-align: center;
	}
</style>
