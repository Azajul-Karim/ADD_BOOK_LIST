<script>
  import { onMount } from "svelte";
  import AddBook from "./components/views/AddBook.svelte";
  import ListBooks from "./components/views/ListBooks.svelte";

  let books = [];
  let message = "";
  let message_type = "";

  function add_new_book(event) {
    let { book } = event.detail;
    if (!book.title || !book.author || !book.isbn) {
      showAlert("Please fill in all fields", "danger");
    } else {
      books = [...books, book];
      localStorage.setItem("books", JSON.stringify(books));
      showAlert("Book Added", "success");
    }
  }

  function showAlert(msg, msg_t) {
    message = msg;
    message_type = msg_t;
    setTimeout(() => {
      message = "";
      message_type = "";
    }, 3000);
  }

  function deleteBook(event) {
    let { book_index } = event.detail;
    books.splice(book_index, 1);
    books = books;
    localStorage.setItem("books", JSON.stringify(books));
  }

  onMount(() => {
    if (localStorage.getItem("books") === null) {
      books = [];
    } else {
      books = JSON.parse(localStorage.getItem("books"));
    }
  });
</script>

<body>
  <div class="container mt-4">
    <h1 class="display-4 text-center">
      <i class="fas fa-book-open text-primary" /> My<span class="text-primary"
        >Book</span
      >List
    </h1>
    {#if message}
      <div class="alert alert-{message_type}">{message}</div>
    {/if}
    <AddBook on:add_book={add_new_book} />

    <ListBooks on:delete_book={deleteBook} {books} />
  </div>
</body>
