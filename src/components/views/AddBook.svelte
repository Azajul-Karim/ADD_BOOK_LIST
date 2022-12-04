<script>
  import { createEventDispatcher } from "svelte";
  let fire = createEventDispatcher();
  let book = {
    title: "",
    author: "",
    isbn: "",
  };

  function addBook(event) {
    event.preventDefault();
    fire("add_book", { book });
    book = {
      title: "",
      author: "",
      isbn: "",
    };
  }
</script>

<form id="book-form" on:submit={(event) => addBook(event)}>
  <div class="form-group">
    <label for="title">Title</label>
    <input
      type="text"
      id="title"
      class="form-control"
      bind:value={book.title}
    />
  </div>
  <div class="form-group">
    <label for="author">Author</label>
    <input
      type="text"
      id="author"
      class="form-control"
      bind:value={book.author}
    />
  </div>
  <div class="form-group">
    <label for="isbn">ISBN#</label>
    <input type="text" id="isbn" class="form-control" bind:value={book.isbn} />
  </div>

  <input type="submit" value="Submit" class="btn btn-primary btn-block" />
</form>
