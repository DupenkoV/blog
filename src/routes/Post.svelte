<script>
	import { createEventDispatcher } from 'svelte';
	import PostText from './PostText.svelte';
	export let title;
	export let author;
	export let date;
	export let post;
	export let id;
	export let editPost;
	export let editingDate;
	let seeText = false;
	const dispatch = createEventDispatcher();
</script>

<!-- Компонент отвечается за рэндэр карточки карточки поста -->

<div>
	<button
		title="Развернуть пост"
		on:click={() => {
			seeText = !seeText;
		}}><h2>{title}</h2></button
	>
	<hr />
	{#if seeText}
		<PostText {post} {id} on:edit={editPost} />
		<hr />
	{/if}

	<p><span>Автор:</span> {author}</p>
	<p><span>Дата создания:</span> {date}</p>
	{#if editingDate}
		<p><span>Дата дата редактирования:</span> {editingDate}</p>
	{/if}
	<button class="deletePost" title="Удалить пост" on:click={() => dispatch('delete', id)}>🗑️</button
	>
</div>

<style>
	div {
		width: 30%;
		border: 1px gray solid;
		border-radius: 5px;
		padding: 5px;
		word-wrap: break-word;
		box-shadow: inset 0 -3em 3em rgba(0, 0, 0, 0.1), 0 0 0 2px rgb(255, 255, 255),
			0.3em 0.3em 1em rgba(0, 0, 0, 0.3);
	}
	h2 {
		margin: 0;
		text-decoration: underline;
	}
	span {
		color: gray;
		font-size: 10px;
	}
	button {
		display: block;
		background-color: inherit;
		border: none;
		cursor: pointer;
		width: 100%;
	}
	p {
		margin: 2px 0;
		font-size: 10px;
	}
	.deletePost {
		width: 30px;
		margin: 0 auto;
	}
</style>
