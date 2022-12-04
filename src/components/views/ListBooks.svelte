<script>
  import { createEventDispatcher } from "svelte";
  import DeleteButton from "../helpers/DeleteButton.svelte";
  let fire = createEventDispatcher();

  export let books = [];

  function deleteBook(event, index) {
    fire("delete_book", { book_index: index });
  }

  // function createdAt() {
  //   let newDate = new Date();
  //   let date = newDate.toLocaleDateString();
  //   let time = newDate.toLocaleTimeString();
  //   return `${date}  ${time}`;
  // }

  function CreatedDate() {
    let newDate = new Date();
    return newDate.toLocaleDateString();
  }

  function CreatedTime() {
    let newDate = new Date();
    return newDate.toLocaleTimeString();
  }
</script>

<table class="table table-striped mt-5">
  <thead>
    <tr>
      <th>Title</th>
      <th>Author</th>
      <th>ISBN#</th>
      <th>Created At</th>
      <th />
    </tr>
  </thead>
  <tbody>
    {#each books as book, i}
      <tr class="text-capitalize font-weight-bold">
        <td>{book.title}</td>
        <td>{book.author}</td>
        <td>{book.isbn}</td>
        <td>{CreatedDate()} <br /> {CreatedTime()}</td>
        <td class="text-right">
          <DeleteButton on:delete={(event) => deleteBook(event, i)} />
        </td>
      </tr>
    {/each}
  </tbody>
</table>
