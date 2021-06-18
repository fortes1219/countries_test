<template>
    <div class="row vertical">
      <el-form label-width="6rem">
        <el-form-item label="Country:" data-width="30rem">
          <div class="row horizontal v_center">
          <el-input
            v-model="searchCountries"
            type="text"
            placeholder="Enter Country's name here"
          />
          <el-button type="primary" data-space-before="0.5rem">Search</el-button>
          </div>
        </el-form-item>
      </el-form>
      <el-pagination
        @current-change="pageChange"
        :current-page.sync="getPagination.currentPage"
        :page-size="pageSize"
        layout="total, prev, pager, next"
        :total="getPagination.totalNum">
      </el-pagination>
    </div>
</template>

<script>
import { mapState, mapMutations, mapGetters, mapActions } from 'vuex'
export default {
  name: 'searchField',
  props: {
    searchCountries: {
      type: String,
      default: ''
    }
  },

  data() {
    return {
      currentPage: 1,
      pageSize: 25,
      totalNum: 0
    }
  },

  computed: {
    ...mapGetters([
      'getPagination'
    ])
  },

  methods: {
    pageChange() {
      
    }
  },


}
</script>