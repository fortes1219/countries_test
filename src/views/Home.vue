<template>
  <!--
    - 目錄必須顯示欄位,()内為Api資料物件的屬性
		- 國旗(圖片資源請使用 flag)
		- 國家名稱（name）
		- 2位國家代碼(alpha2Code)
		- 3位國家代碼(alpha3Code)
		- 母語名稱(nativeName)
		- 替代國家名稱(altSpellings)
		- 國際電話區號(callingCodes)
    - 以國名搜尋功能(模糊搜尋)
    - 以國名排序功能（正序、倒序）
    - 分頁(每頁25筆)
    - 點擊國家名稱后顯示一個Modal，裏面顯示該國家的其他資訊。
  -->
  <div class="outer" data-inset="1rem">
    <searchField
      :searchCountries="search"
    />
    <div class="row horizontal space wrap" data-row-count="5">
      <div v-for="(item, i) in getResponse" :key="i" class="data_row" data-inset="0.5rem">
        <div class="country_items">
          <span class="row horizontal v_center" data-border-bottom="light-gray">
            <img :src="`https://www.countryflags.io/${item.alpha2Code}/shiny/64.png`">
            <b>{{ item.name }}</b>
          </span>
          <div class="row horizontal v_center" data-space-vertical="0.5rem">
            <span class="tags">{{ item.alpha2Code }}</span>
            <span class="tags">{{ item.alpha3Code }}</span>
          </div>
          <div class="info">
            <span>{{ item.nativeName }}</span>
            <span>{{ item.altSpellings.join(',') }}</span>
            <span>{{ item.callingCodes.join(',') }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState, mapMutations, mapGetters, mapActions } from 'vuex'
import searchField from '@/components/searchField.vue'
export default {
  name: 'Home',
  components: {
   searchField
  },
  data() {
    return {
      search: '',
      showResult: [],
    }
  },

  computed: {
    ...mapGetters([
      'getResponse',
    ])
  },
  methods: {
    ...mapActions([
      'FETCH_API',
    ]),
    ...mapMutations([
      'SET_SEARCH_KEYWORDS'
    ]),
    async init() {
      await this.FETCH_API()
    },
    async handleSearch() {
      await this.SET_SEARCH_KEYWORDS('')
      await this.FETCH_API()
    }
  },
  created() {
    this.init()
  },

  mounted() {

  },
}
</script>
