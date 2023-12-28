<script setup>
import axios from 'axios';

// 请求接口
axios.get('http://192.168.110.87:8000/project/list')
  .then(function (response) {
    // 处理请求成功的结果
    console.log(response.data)
    const tableData = response.data
    
  })
  .catch(function (error) {
    // 处理请求失败的结果
    console.log("请求失败，原因是",error)
  });

</script>

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
            <el-table-column prop="Project_Name" label="项目名称"  />
            <el-table-column prop="Project_CreatedBy" label="创建人" />
            <el-table-column prop="Project_Description" label="创建时间" />
          </el-table>
        </el-scrollbar>
      </el-main>
    </el-container>
  </el-container>
</template>

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

