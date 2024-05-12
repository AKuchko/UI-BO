<template>
  <div class="base-autocomplete">
    <input type="text" class="base-autocomplete__input">
  </div>
</template>

<script>
import Sender from '~/api/sender';

export default {
  name: 'base-autocomplete',
  model: {
    prop: 'value',
    event: 'input',
  },
  props: {
    value: { type: String, default: '' },
    label: { type: String, default: '' },
    error: { type: String, default: '' },
    path: { type: String, default: '' },
    baseUrl: { type: String, default: '/autocomplete' },
    idProperty: { type: String, default: 'id' },
    labelProperty: { type: String, default: 'label' },
    disabledProperty: { type: String, default: 'disabled' },
    required: { type: Boolean, default: false },
    isError: { type: Boolean, default: false },
    multiple: { type: Boolean, default: false },
    backSearch: { type: Boolean, default: false },
    backLoad: { type: Boolean, default: false },
    formatFunc: { type: Function, default: (data) => data },
    filterFunc: { type: Function, default: () => true },
    mapFunc: { type: Function, default: (item) => item },
    onInputFunc: { type: Function, default: () => true },
    params: { type: Object, default: () => ({}) },
    items: { type: Array, default: () => [] },
  },
  data () {
    return {
      sender: new Sender(),
      term: '',
      active: false,
      filled: false,
      focused: false,
      loading: false,
      randomId: null,
      selectedItem: null,
      allItems: [],
      selectedItems: [],
      filteredItems: [],
    };
  },
  computed: {
    selectedItemsValues () {
      return this.selectedItems.map(item => item[this.idProperty]);
    },
  },
  async mounted () {
    this.loading = true;

    this.createRandomId();
    await this.init();

    this.loading = false;
  },
  methods: {
    async init () {
      this.allItems = this.backLoad
        ? await this.loadData()
        : this.items;

      this.fill(this.value);
    },
    async loadData (term = '') {
      const { data } = await this.sender.get(`${this.baseUrl}/${this.path}`);

      if (!data || !data.length) return [];

      const formattedData = this.formatFunc(data);

      return formattedData.filter(this.filterFunc);
    },
    fill (value) {
      if (!value || (this.multiple && !value.length))
        return this.clean();

      if (this.multiple)
        return this.fillMultiple();

      this.fillOne();
    },
    fillMultiple (value) {

    },
    fillOne (value) {

    },
    createRandomId () {
      this.randomId = String(Math.random());
    },
  }
};
</script>

<style lang="scss">
  .base-autocomplete {

  }
</style>
