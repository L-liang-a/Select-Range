<template>
    <div style="width: 1200px;margin: 0 auto;">
        <!-- <a-button>反选</a-button> -->
        <a-table :row-selection="rowSelection" :columns="columns" :data-source="data" />
    </div>
</template>

<script>
const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
  },
  {
    title: 'Age',
    dataIndex: 'age',
  },
  {
    title: 'Address',
    dataIndex: 'address',
  },
];

const data = [];
for (let i = 0; i < 46; i++) {
  data.push({
    key: i,
    name: `Edward King ${i}`,
    age: 32,
    address: `London, Park Lane no. ${i}`,
  });
}
export default {
name: 'List',
components: {},
props: {},
data () {
    return {
        data,
        columns,
        selectedRowKeys: [], // Check here to configure the default column
    }
},
computed: {
    rowSelection() {
      const { selectedRowKeys } = this;
      return {
        selectedRowKeys,
        onChange: this.onSelectChange,
        selections: true,
        onSelection: this.onSelection,
      };
    },
},
watch: {},
mounted () {},
created () {},
methods: {
    onSelectChange(selectedRowKeys) {
      console.log('selectedRowKeys changed: ', selectedRowKeys);
      this.selectedRowKeys = selectedRowKeys;
    },
    getCheckboxProps (v) {
        console.log(v);
    }
},

}
</script>

<style lang='less' scoped>
</style>