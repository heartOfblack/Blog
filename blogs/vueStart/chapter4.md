---
title: 3 创建菜单
date: 2021-8-5
categories:
 - vue从零搭建业务管理 
---



> 前情提要：上一个章节已经安装了element-ui，因此我们会创建后台管理用菜单。目前，暂不涉及数据的存储，也就是不涉及后端和数据库内容。以本地mock数据的形式读取数据。后续再根据情况，考虑是否加入koa及数据库内容维护数据。
>
> 在src，目录下新建一个mock数据，创建menu.js存放假数据
>
> 数据格式为：[
>
> {
>
>   icon: '',//图表
>
>   id: 26685,//当前节点ID
>
>   label: '首页',//当前菜单节点名称
>
>   parentId: 13,//父级ID
>
>   parentLabel: '父级菜单名称',
>
>   status: 1,
>
>   treeNo: '0400',
>
>   type: 0,
>
>   url: '/',//对应路由
>
>   weight: 1，//权重
>
> children: [ //子菜单
>
> {
>
> //结构与父级一致
>
> }]
>
>  }
>
> ]



> 由于这系列文章的目的，是为了熟悉基本的脚手架、各种配置、后台管理系统的基本设计思路，讲解简单的思路，实际情况可能会根据不同的业务，采用不同的结构，上述菜单结构中，目前只需要用到几个字段：label,children,url，其余字段不做处理。



一般情况下，管理系统的菜单层级不会特别深，在做菜单的自己时，根据自己的业务，直接根据菜单层级写代码。 但是，考虑到后续的拓展，菜单还是利用递归的方式，创建无限制层级菜单。代码如下：

```vue
<!--menu.vue-->
<template>
  <el-menu default-active="/" unique-opened :collapse="isCollapse" :router="true">
  <template v-for="item in menuList">
    <menu-item :item="item" :key="item.id"></menu-item>
  </template>
  </el-menu>
</template>
```

```vue
<!--menuItem.vue-->
<template>
  <el-submenu v-if="item.children" :index="item.url" :key="item.id">
    <template slot="title">
      <i class="el-icon-location"></i>
      <span>{{item.label}}</span>
    </template>
   <menu-item v-for="subItem in item.children" :purl="item.url" :item="subItem" :key="subItem.id"></menu-item>  <!-- -->
  </el-submenu>
  <el-menu-item v-else :index="purl ? purl +'/'+item.url : item.url" :key="item.id">
    <template slot="title">
      <i class="el-icon-location"></i>
      <span>{{item.label}}</span>
    </template>
  </el-menu-item>
</template>
<script>
export default {
    name: 'menuItem',
  components: {
    MenuItem: () => import('./MenuItem')/** 组件的循环嵌套调用需要异步,否则会有报错提示，或者你可以按正常引入的方式，不过需要为menuItem设置name属性，这样vue才能正确处理。详情请查看vue官方网站的边界情况，循环引用-递归组件 */
  },
  props: {
    item: {
      type: Object,
      default: () => ({})
    },
    purl: {
      type: String,
      default: ''
    }
  },
  data () {
    return {}
  }
}

</script>
```

组件是可以引入自身的，前提是，该组件的引入一定要有结束条件，即不能无限死循环，此处菜单递归完，便结束调用。

