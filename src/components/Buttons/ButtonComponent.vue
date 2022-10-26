<template>
  <div class="btn__container">
    <button class="btn__action"><img src="@/assets/delete.png" alt=""></button>
    <button class="btn__action"><img src="@/assets/Vector.png" alt=""></button>
    <button class="btn__action handle"><img src="@/assets/remuve.png" alt=""></button>
  </div>
</template>

<script>
export default {
};
</script>

<style>
  .btn__action {
    background-color: white;
    border: unset;
    padding: unset;
    cursor: pointer;
  }

  .btn__container {
    display: flex;
    gap: 21px;
  }
</style>
