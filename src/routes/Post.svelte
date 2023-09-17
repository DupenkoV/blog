<script>
	import PostText from './PostText.svelte';
	export let title;
	export let author;
	export let date;
	export let post;
	export let id;
	export let editPost;
	export let editingDate;
	let seeText = false;
</script>

<!-- Компонент отвечается за рэндэр карточки карточки поста -->

<div>
	<button
		on:click={() => {
			seeText = !seeText;
		}}><h2>{title}</h2></button
	>
	{#if seeText}
		<PostText {post} {id} on:edit={editPost} />
	{/if}
	<p><span>Автор:</span> {author}</p>
	<p><span>Дата создания:</span> {date}</p>
	{#if editingDate}
		<p><span>Дата дата редактирования:</span> {editingDate}</p>
	{/if}
</div>

<style>
	div {
		width: 30%;
		border: 1px gray solid;
		border-radius: 5px;
		padding: 5px;
		word-wrap: break-word;
	}
	h2 {
		margin: 0;
	}
	span {
		color: gray;
		font-size: 10px;
	}
	button {
		display: block;
		background-color: white;
		border: none;
		cursor: pointer;
	}
</style>
