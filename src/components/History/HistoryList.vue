<template>
  <HistoryListUI
    :history="history"
    :status="status"
    :canLoadMore="canLoadMore"
    :fetchMore="fetchMore"
    />
</template>
<script>
import HistoryListUI from '@/components/History/HistoryListUI'
import { mapActions, mapGetters } from 'vuex'
export default {
  props: {
    user: { required: false },
    store: { required: false },
    group: { required: false },
  },
  computed: mapGetters({
    history: 'history/all',
    status: 'history/receiveStatus',
    canLoadMore: 'history/canLoadMore',
  }),
  methods: mapActions({
    fetchMore: 'history/fetchMore',
    fetchForUser: 'history/fetchForUser',
    fetchForGroup: 'history/fetchForGroup',
    fetchForStore: 'history/fetchForStore',
  }),
  mounted () {
    if (this.user) this.fetchForUser(this.user)
    else if (this.group) this.fetchForGroup(this.group)
    else if (this.store) this.fetchForStore(this.store)
  },
  watch: {
    user () { this.fetchForUser(this.user) },
    group () { this.fetchForGroup(this.group) },
    store () { this.fetchForGroup(this.store) },
  },
  components: { HistoryListUI },
}
</script>
