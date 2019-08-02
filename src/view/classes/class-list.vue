<template>
  <Table :columns="columns"
         :data="tabledata">
    <template slot-scope="{ row, index }"
              slot="name">
      <Input type="text"
             v-model="editName"
             v-if="editIndex === index" />
      <span v-else>{{ row.name }}</span>
    </template>

    <template slot-scope="{ row, index }"
              slot="age">
      <Input type="text"
             v-model="editAge"
             v-if="editIndex === index" />
      <span v-else>{{ row.age }}</span>
    </template>

    <template slot-scope="{ row, index }"
              slot="birthday">
      <Input type="text"
             v-model="editBirthday"
             v-if="editIndex === index" />
      <span v-else>{{ row.birthday }}</span>
    </template>

    <template slot-scope="{ row, index }"
              slot="address">
      <Input type="text"
             v-model="editAddress"
             v-if="editIndex === index" />
      <span v-else>{{ row.address }}</span>
    </template>

    <template slot-scope="{ row, index }"
              slot="action">
      <div v-if="editIndex === index">
        <Button @click="handleSave(index)">保存</Button>
        <Button @click="editIndex = -1">取消</Button>
      </div>
      <div v-else>
        <Button type="primary"
                size="small"
                style="margin-right: 5px"
                @click="handleEdit(row,index)">编辑</Button><Button type="error"
                size="small"
                @click="remove(index)">删除</Button>
      </div>
    </template>
  </Table>
</template>
<script>
//columns 表头
export default {
  data() {
    return {
      columns: [
        {
          title: "班级",
          slot: "name"
        },
        {
          title: "人数",
          slot: "age"
        },
        {
          title: "任课老师",
          slot: "birthday"
        },
        {
          title: "班主任",
          slot: "address"
        },
        {
          title: "操作",
          slot: "action"
        }
      ],
      tabledata: [
        //表格对应的数据
        {
          name: "1709A",
          age: 14,
          birthday: "阮老师",
          address: ""
        },
        {
          name: "1807A",
          age: 26,
          birthday: "宋老师",
          address: "李老师"
        },
        {
          name: "1808B",
          age: 14,
          birthday: "阮老师",
          address: "崔老师"
        },
        {
          name: "1810A",
          age: 22,
          birthday: "施老师",
          address: "李老师"
        }
      ],
      editIndex: -1, // 当前聚焦的输入框的行数
      editName: "", // 第一列输入框，当然聚焦的输入框的输入内容，与 data 分离避免重构的闪烁
      editAge: "", // 第二列输入框
      editBirthday: "", // 第三列输入框
      editAddress: "" // 第四列输入框
    };
  },
  created() {
    //  console.log(this.$route.query.obj)
     if(typeof this.$route.query.obj==='object'){
       this.tabledata.push(this.$route.query.obj)
     }
  },
  methods: {
    handleEdit(row, index) {
      this.editName = row.name;
      this.editAge = row.age;
      this.editAddress = row.address;
      this.editBirthday = row.birthday;
      this.editIndex = index;
    },
    handleSave(index) {
      this.tabledata[index].name = this.editName;
      this.tabledata[index].age = this.editAge;
      this.tabledata[index].birthday = this.editBirthday;
      this.tabledata[index].address = this.editAddress;
      this.editIndex = -1;
    },
    getBirthday(birthday) {
      const date = new Date(parseInt(birthday));
      const year = date.getFullYear();
      const month = date.getMonth() + 1;
      const day = date.getDate();
      return `${year}-${month}-${day}`;
    },
    remove(index) {
      this.tabledata.splice(index, 1);
    }
  }
};
</script>