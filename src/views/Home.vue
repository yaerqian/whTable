<template>
  <div>
    在这里引入表格组件
    <test-render
      :columns="columns"
      :data="tableData"
      :size="size"
      @handleClick="handleClick"
      @edit="edit"
      @del="del"
    ></test-render>
  </div>
</template>

<script>
import testRender from "@/components/testRender";
export default {
  data() {
    return {
      size: "mini",
      columns: [
        { label: "日期", prop: "date" },
        { label: "姓名", prop: "name" },
        { label: "地址", prop: "address" },
        {
          label: "年龄",
          prop: "age",
          templateInfo: {
            classify: ["el-input"],
            disabled: [false]
          }
        },
        {
          label: "年级",
          prop: "grade",
          templateInfo: {
            classify: ["el-select"],
            disabled: [false],
            option:[
              [
                {label: '一年级', value: 1,id: 1},
                {label: '二年级', value: 2,id: 2},
                {label: '三年级', value: 3,id: 3},
              ]
            ]
          }
        },
        {
          label: "操作",
          prop: "operating",
          templateInfo: {
            classify: ["el-button", "el-button"],
            content: ["编辑", "删除"],
            type: ["primary", "danger"],
            event: ["edit", "del"],
            disabled: ["scope.row.id == 1", "scope.row.id == 2"]
          }
        }
      ],
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          grade:1,
          age: '33',
          id: 1
        },
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          grade:'',
          age: '',
          id: 2
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄",
          grade:'',
          age: '',
          id: 3
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄",
          grade:'',
          age: '',
          id: 4
        }
      ]
    };
  },
  components: {
    "test-render": testRender
  },
  methods: {
    handleClick(data) {
      console.log(data);
    },
    edit(data) {
      console.log(data);
    },
    del(data) {
      console.log(data);
    }
  }
};
</script>

<style>
</style>
