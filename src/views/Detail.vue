<template>
  <div>
    <Loader v-if="loading" />
    <div v-else-if="record">
      <div class="breadcrumb-wrap">
        <router-link to="/history" class="breadcrumb">{{'Detail_History' | localize}}</router-link>
        <a @click.prevent class="breadcrumb">
          {{ record.type === 'income' ? 'History_Income' : 'History_Outcome' | localize }}
        </a>
      </div>
      <div class="row">
        <div class="col s12 m6">
          <div class="card" :class="{
            'red': record.type === 'outcome',
            'green': record.type === 'income'
          }">
            <div class="card-content white-text">
              <p>{{'Detail_Description' | localize}}: {{ record.description }}</p>
              <p>{{'Detail_Amount' | localize}}: {{ record.amount |currency }}</p>
              <p>{{'Detail_Category' | localize}}: {{ record.categoryName }}</p>

              <small>{{ record.date | date('datetime') }}</small>
            </div>
          </div>
        </div>
      </div>
    </div>
    <p class="center" v-else>{{'Detail_Record' | localize}} id={{$route.params.id}} {{'Detail_Not_Found' | localize}}</p>
  </div>
</template>

<script>
export default {
  name: 'detail',
  metaInfo() {
    return {
      title: this.$title('Detail_Title')
    }
  },
  data: () => ({
    record: null,
    loading: true
  }),
  async mounted() {
    const id = this.$route.params.id
    const record = await this.$store.dispatch('fetchRecordById', id)
    const category = await this.$store.dispatch('fetchCategoryById', record.categoryId)

    this.record = {
      ...record,
      categoryName: category.title
    }

    this.loading = false
  }
}
</script>