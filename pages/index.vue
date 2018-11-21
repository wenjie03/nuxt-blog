<template>
  <el-container style="height: 100vh; border: 1px solid #eee">
    <el-aside 
      width="200px" 
      style="background-color: rgb(238, 241, 246)"
    >
      <el-menu>
        <el-submenu 
          v-for="(el, index) in menuData" 
          :key="index" 
          :index="index"
        >
          <template slot="title">
            <i class="el-icon-message" />
            {{ el.title }}
          </template>
          <el-menu-item-group 
            v-for="(item, index) in el.children"
            :key="index"
          >
            <template slot="title">{{ item.title }}</template>
            <el-menu-item 
              v-for="(child, index) in item.children"
              :key="index"
  
              :index="'1-' + index"
            >{{ item.title }}</el-menu-item>

          </el-menu-item-group>
        </el-submenu>
      </el-menu>
    </el-aside>

    <el-container>
      <el-header style="text-align: right; font-size: 12px">
        <el-dropdown>
          <i 
            class="el-icon-setting" 
            style="margin-right: 15px" 
          />
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>查看</el-dropdown-item>
            <el-dropdown-item>添加</el-dropdown-item>
            <el-dropdown-item>删除</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
        <span>李</span>
      </el-header>

      <el-main>

        <ul>
          <li
            v-for="(item, index) in tableData"
            :key="index">
            <h1>{{ item.name }}</h1>
            <p>{{ item.date }}</p>
            <span>{{ item.address }}</span>
          </li>
        </ul>
        <el-table :data="tableData">
          <el-table-column 
            prop="date" 
            label="Date" 
            width="140" 
          />
          <el-table-column 
            prop="name" 
            label="Name" 
            width="120" 
          />
          <el-table-column 
            prop="address" 
            label="Address" 
          />
        </el-table>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData() {
    let data = await axios.get('http://s.kongque360.cn/static/home.json')
    data = data.data
    return {
      tableData: data.data,
      menuData: data.menu
    }
  }
}
</script>

<style>
.el-header {
  background-color: #b3c0d;
  color: #333;
  line-height: 60px;
}

.el-aside {
  color: #333;
}
</style>
