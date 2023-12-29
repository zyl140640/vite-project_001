<template>
  <el-container class="layout-container-demo" style="height: 500px">
    <el-aside width="200px">
      <el-scrollbar>
        <el-menu :default-openeds="['1', '3']">
          <el-sub-menu index="1">
            <template #title>
              <el-icon><message /></el-icon>项目中心
            </template>
            <el-menu-item-group>
              <!-- <template #title>Group 1</template> -->
              <el-menu-item index="1-1">项目管理</el-menu-item>
              <el-menu-item index="1-2">用例管理</el-menu-item>
              <el-menu-item index="1-3">步骤管理</el-menu-item>
              <el-menu-item index="1-4">测试报告</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
        </el-menu>
      </el-scrollbar>
    </el-aside>

    <el-container>
      <el-header style="text-align: right; font-size: 12px">
        <div class="toolbar">
          <el-dropdown>
            <el-icon style="margin-right: 8px; margin-top: 1px"
              ><setting
            /></el-icon>
            <template #dropdown>
              <el-dropdown-menu>
                <el-dropdown-item>View</el-dropdown-item>
                <el-dropdown-item>Add</el-dropdown-item>
                <el-dropdown-item>Delete</el-dropdown-item>
              </el-dropdown-menu>
            </template>
          </el-dropdown>
          <span>Tom</span>
        </div>
      </el-header>

      <el-main>
        <el-scrollbar>
          <el-table :data="tableData">
            <el-table-column prop="id" label="序号"  />
            <el-table-column prop="project_name" label="项目名称"  />
            <el-table-column prop="Project_creator" label="项目创建人" />
            <el-table-column prop="Project_creation_time" label="项目创建时间" />
          </el-table>
        </el-scrollbar>
      </el-main>
    </el-container>
  </el-container>
</template>



<script>
import axios from 'axios';

export default {
  data() {
    return {
      tableData: []  // 初始化表格数据为空数组
    };
  },
  mounted() {
    // 在组件挂载后，进行接口请求
    this.fetchData({ yourQueryParam: 'value' }); // 传递查询参数
  },
  methods: {
    async fetchData(params) {
      try {
        // 使用axios的params选项传递查询参数
        const response = await axios.get('http://192.168.110.87:8000/project/list', {
          params: params
        });
        const dataArray = Object.values(response.data);
        // 更新tableData的值，使其等于接口返回的数据
        console.log('Response data:', response.data);
        console.log('转化成数组的对象:', dataArray[0]);
        this.tableData = dataArray[0];
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    }
  }
};
</script>


<style scoped>
.layout-container-demo .el-header {
  position: relative;
  background-color: var(--el-color-primary-light-7);
  color: var(--el-text-color-primary);
}
.layout-container-demo .el-aside {
  color: var(--el-text-color-primary);
  background: var(--el-color-primary-light-8);
}
.layout-container-demo .el-menu {
  border-right: none;
}
.layout-container-demo .el-main {
  padding: 0;
}
.layout-container-demo .toolbar {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  right: 20px;
}
</style>

