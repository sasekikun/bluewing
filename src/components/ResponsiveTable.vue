<template>
  <table :class="className">
    <tr v-for="(item, index) in items" :key="index">
      <th>{{ item.th }}</th>
      <td>{{ item.td }}</td>
    </tr>
  </table>
</template>

<script>
export default {
  name: 'ResponsiveTable',
  props: {
    items: {
      type: Array,
      default: () => []
    },
    className: {
      type: String,
      default: 'gray_style'
    }
  }
}
</script>

<style lang="scss" scoped>
table {
  width: 100%;
  border-collapse: collapse;
  th {
    font-weight: normal;
  }
}

@media screen and (min-width: 768px) {
  th {
    width: 30%;
  }
  td {
    width: 70%;
  }
}

@media screen and (max-width: 768px) {
  table,
  tr,
  th,
  td {
    display: block;
  }
}

.gray_style {
  tr:nth-child(odd) {
    background: #eee;
  }

  tr:nth-child(even) {
    background: #fff;
  }

  th {
    text-align: left;
  }

  th,
  td {
    padding: 8px 16px;
  }

  @media screen and (max-width: 767px) {
    tr {
      background: #fff !important;
    }

    th {
      background: #eee;
    }
  }
}

.border_style {
  background: #fff;
  tr {
    border-bottom: 1px solid #666;
    &:last-child {
      border: none;
    }
  }
  th,
  td {
    padding: 16px;
  }
  @media screen and (max-width: 767px) {
    th {
      text-align: left;
      padding-bottom: 0;
    }
    td {
      padding-top: 8px;
    }
  }
}
</style>
