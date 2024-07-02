<script>
  import Header from "$lib/Header.svelte";

  let books = [
    // { nameBook: "Daisy Jones", read: false },
    // { nameBook: "A Little Life", read: false },
  ];
  //an array that will hold the list of books. ( Array starting point)

  function addBook() {
    //addbook is a function that adds a new empty string to the books array whenever it is called.(function annoucement/declaration)
    // books = [...books, ""];
    books = [...books, { nameBook: "", read: false }];
    // ... books= expanding the stuff in the array laready
    // { nameBook: "", read: false }= adds a blank object at the end, the oibject contains 2 properites
  }

  function saveBooks() {
    localStorage.bookList = JSON.stringify(books);
  }

  function loadBooks() {
    const booksAsJSON = localStorage.bookList;
    const booksAsArray = JSON.parse(booksAsJSON);
    books = booksAsArray;
  }
</script>

<Header />

<button on:click={addBook}> Add Book</button>

<button on:click={saveBooks}> Save Books</button>

<button on:click={loadBooks}> Load Books</button>

{#each books as book, index}
  <div class="bookRead">
    <!-- <div class="book"> -->
    <input bind:value={books[index].nameBook} />
    <!-- <input bind:value={bookinput[index]nameBook} /> -->
    <!-- </div> -->
    <input type="checkbox" bind:checked={books[index].read} />
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
