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
    // ... books= expanding the stuff in the array already
    // { nameBook: "", read: false }= adds a blank object at the end, the oibject contains 2 properites
  }

  function saveBooks() {
    localStorage.bookList = JSON.stringify(books);
    //local storage is an API that allows you to store key-value pairs in a web browser. Data stored in localStorage has no expiration time, meaning it will stay until it's deleted.
    //The JSON string representation of the tasks array is stored in localStorage under the key todos. This means that the tasks array is saved as a string in the browser's local storage and can be retrieved later.
  }

  function loadBooks() {
    const booksAsJSON = localStorage.bookList;
    // localStorage.bookList: This gets the value stored in localStorage under the key bookList. This is the JSON string that was previously saved by the saveBooks function.
    const booksAsArray = JSON.parse(booksAsJSON);
    // The JSON.parse function converts the JSON string back into the array of books.
    books = booksAsArray;
    // This overwrites the books array with the books that were previously saved.
  }

  let lists = [
    {
      name: "Books",
      list: ["Diasy Jones", "the Silent P"],
    },
    {
      name: "Recipe",
      list: ["eats", "food"],
    },
  ];
  let selected = lists[0];
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

{selected}
<!-- tests that it works -->
<select bind:value={selected}>
  {#each lists as list}
    <option value={list}> {list.name}</option>
  {/each}
</select>
{#each selected.list as item, index}
  <input bind:value={selected.list[index]} />
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
