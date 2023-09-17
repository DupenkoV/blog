<script>
	import Post from './Post.svelte';
	let dataLS;

	if (typeof window !== 'undefined') {
		dataLS = JSON.parse(localStorage.getItem('posts'));
	}

	let title = '';
	let post = '';
	let author = '';

	// Массив постов формируется из localStorage.
	let posts = dataLS ? dataLS : [];

	// Функция получения поста блога и добавления в массив постов и localStorage
	const submitForm = () => {
		const newPost = {
			id: Math.floor(Math.random() * 10000).toString(),
			post,
			author,
			title,
			date: new Date().toLocaleString(),
			editingDate: ''
		};
		posts = [newPost, ...posts];
		localStorage.posts = JSON.stringify(posts);
		title = '';
		post = '';
		author = '';
	};

	// Функция внесения изменений в текст поста
	function editPost(post) {
		posts = posts.map((item) => {
			if (item.id !== post.detail.id) {
				return item;
			} else {
				return {
					...item,
					post: post.detail.post,
					editingDate: new Date().toLocaleString()
				};
			}
		});
		localStorage.posts = JSON.stringify(posts);
	}

	// Функция удаления поста
	function deletePost(post) {
		posts = posts.filter((item) => item.id != post.detail);
		localStorage.posts = JSON.stringify(posts);
	}
</script>

<h1>Блог</h1>
<form on:submit|preventDefault={submitForm}>
	<input
		name="title"
		type="text"
		placeholder="Введите заголовок поста"
		required
		autocomplete="off"
		bind:value={title}
	/>
	<br />
	<textarea
		name="post"
		placeholder="Введите сообщение"
		required
		autocomplete="off"
		bind:value={post}
	/>
	<br />
	<input
		name="author"
		type="text"
		placeholder="Введите ник автора"
		required
		autocomplete="off"
		bind:value={author}
	/>
	<button type="submit">Добавить пост</button>
</form>
<hr />
<div class="wrapper">
	{#each posts as post}
		<Post {...post} {editPost} on:delete={deletePost} />
	{/each}
</div>

<style>
	h1 {
		text-align: center;
	}
	form {
		text-align: center;
		width: 30%;
		box-shadow: inset 0 -3em 3em rgba(0, 0, 0, 0.1), 0 0 0 2px rgb(255, 255, 255),
			0.3em 0.3em 1em rgba(0, 0, 0, 0.3);
		padding: 10px 0;
		margin: 0 auto;
	}
	textarea {
		width: 90%;
		height: 10rem;
		padding: 1rem;
		margin: 1rem 0;
	}
	input {
		width: 50%;
	}
	.wrapper {
		display: flex;
		align-items: center;
		flex-direction: column;
		margin-top: 20px;
		gap: 10px;
	}
</style>
