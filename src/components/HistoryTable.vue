<template>
  <table>
    <thead>
    <tr>
      <th>№</th>
      <th>{{'HistoryTable_Amount' | localize}}</th>
      <th>{{'HistoryTable_Date' | localize}}</th>
      <th>{{'HistoryTable_Category' | localize}}</th>
      <th>{{'HistoryTable_Type' | localize}}</th>
      <th>{{'HistoryTable_Open' | localize}}</th>
    </tr>
    </thead>

    <tbody>
    <tr v-for="(record, idx) of records" :key="record.id">
      <th>{{ idx + 1 }}</th>
      <th>{{ record.amount | currency('BYN') }}</th>
      <td>{{ record.date | date('datetime') }}</td>
      <td>{{ record.categoryName }}</td>
      <td>
        <span
          :class="[record.typeClass]"
          class="white-text badge"
        >{{ record.typeText }}</span>
      </td>
      <td>
        <button
          v-tooltip="'HistoryTable_Open_Record'"
          class="btn-small btn"
          @click="$router.push('/detail/' + record.id)"
        >
          <i class="material-icons">open_in_new</i>
        </button>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script>

export default {
  props: {
    records: {
      required: true,
      type: Array
    }
  }
}
</script>
