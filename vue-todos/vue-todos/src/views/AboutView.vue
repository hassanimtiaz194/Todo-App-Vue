<template>
  <div class="about">
    <h2>Vue Todos</h2>
    <br />
    <p>This app was created using Vue for practice purposes. It includes the following features:</p>
    <br />
    <ul class="aboutList">
      <li>Users can create to-do items.</li>
      <li>Users can edit existing to-do items.</li>
      <li>Users can delete to-do items.</li>
      <li>Created to-do items are stored in localStorage, so the data persists even if the page is refreshed.</li>
    </ul>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    display: flex;
    flex-direction: column;
    max-width: 500px;
    width: 100%;
    margin: 0 auto;
    padding: 40px 16px;
  }
  .aboutList {
    padding-left: 20px;
  }
}
</style>
