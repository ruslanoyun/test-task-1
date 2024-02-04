<template>
  <div>
    <button type="button">Добавить</button>
    <table>
      <tr>
        <th>Имя</th>
        <th>Телефон</th>
      </tr>
      <tr>
        <td>Иван</td>
        <td>89001234567</td>
      </tr>
      <tr>
        <td>Петр</td>
        <td>89006543210</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'UserListPage',
};
</script>

<style scoped>
table {
    border: 1px solid;
}
th, td {
    border: 1px solid;
}
</style>
