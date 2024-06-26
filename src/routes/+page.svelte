<script>
  import Header from "$lib/Header.svelte";
  let isChecked = false;
  let books = [];
  function addBook() {
    books = [...books, ""];
  }

  function saveBooks() {
    const booksAsJSON = JSON.stringify(books);
    localStorage.bookList = booksAsJSON;
  }

  function loadBooks() {
    const booksAsJSON = localStorage.bookList;
    const booksAsArray = JSON.parse(booksAsJSON);
    tasks = booksAsArray;
  }
</script>

<Header />

<h2>SvelteKit</h2>

<button on:click={addBook}> Add Book</button>

<button on:click={saveBooks}> Save Books</button>

<button on:click={loadBooks}> Load Books</button>

{#each books as book, index}
  <div class="bookRead">
    <div class="book">
      <input bind:value={books[index]} />
    </div>
    <input type="checkbox" bind:checked={isChecked} />
    <p>Book is read{isChecked}.</p>
  </div>
{/each}

<footer>
  <p>&copy; Craighead Diocesan School 2024</p>
</footer>

<style>
  .bookRead {
    display: flex;
    align-items: center;
  }
</style>
