<script>
	import Book from './book.svelte';
	import Button from './button.svelte';

	const localStorageBooksKey = 'bookStore.books';

	let title = '';
	let price = 7;
	let description = '';

	function setTitle(event){
		title = event.target.value;
	}


	const storedBooks = JSON.parse(localStorage.getItem(localStorageBooksKey));

	let books = storedBooks!=null?storedBooks:[];


    function addBook(){

		const newBook = {
			title,
            price,
            description
        };

		books = books.concat(newBook);
		localStorage.setItem(localStorageBooksKey, JSON.stringify(books))
    }
</script>

<style>
	h1{
		color: purple;
	}

	section{
		margin: auto;
		width: 30rem;
	}

	label, input, textarea {
		width: 100%;
	}


</style>

<section>
	<div>
		<label for="title">Title</label>
		<input type="text" id="id" value={title} on:input={setTitle} />
	</div>

	<div>
		<label for="price">Price</label>
		<input type="number" id="price" bind:value={price}/>

	</div>
	<div>
		<label for="description">Description</label>
		<textarea rows="3" id="description" bind:value={description}></textarea>
	</div>
	<Button on:click={addBook}>ADD Book</Button>
	{#if books.length === 0}
		<p>
		   No books in stock.
		</p>
	{:else}
		{#each books as book}
			<Book bookTitle={book.title} bookPrice={book.price} bookDescription={book.description}/>
		{/each}
	{/if}
</section>