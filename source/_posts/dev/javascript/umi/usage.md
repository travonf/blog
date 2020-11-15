---
title: umi3.0踩坑记录
date: 2020/10/01 00:00:00
updated: 2020/10/01 00:00:00
tags: "umijs"
categories: ["Develop", "Javascript", "Umi"]
---

新的东西出来总是要尝尝鲜的，在这里把遇到的一些问题记录下来，方便他人避坑。
遇到问题时，多翻翻官方文档，虽然写的很粗（每次翻都血压上升），再翻翻 issues 区，看看有没有前人遇到过相似的问题；
这里有一个演练场，基于 umijs，与本地开发体验一致，可以用来提交问题复现，[点此查看](https://codesandbox.io/s/umi-app-9nizb)
另外我现在会尽量用 ts 来写，这样不用为了查找 API 翻来翻去了；
话不多说，我们进入正题，如有错误，欢迎指正：

<!--more-->

# 布局

umijs 集成了 pro-layout 组件，只需要在配置里开启即可，但是有几个点需要注意：
这里只能配置一些静态属性，如果想动态控制布局，需要在 app.ts 中配置，layout 具有什么配置，我已经写在类型里了：

```javascript
// config/config.ts
import { defineConfig } from "umi";
import layout from "./layout.config";

export default defineConfig({
  layout,
});
```

```javascript
// config/layout.config.ts
import { BasicLayoutProps } from "@ant-design/pro-layout";

// [具体配置说明看这里](https://procomponents.ant.design/components/layout#api)
const layout: BasicLayoutProps = {
  title: "React Awesome",
  logo: "/assets/react.ico",
  pure: false,
  loading: true,
  // menuHeaderRender,
  // onMenuHeaderClick,
  // contentStyle: {
  //   // minHeight: 'calc(100vh - 48px - 124px)',
  //   // padding: 24,
  // },
  layout: "side",
  contentWidth: "Fixed",
  navTheme: "realDark",
  fixedHeader: false,
  fixSiderbar: true,
  breakpoint: "lg",
  menu: { locale: true },
  // iconfontUrl,
  locale: "zh-CN",
  siderWidth: 208,
  // onCollapse,
  // onPageChange,
  // headerRender,
  // headerTitleRender,
  // headerContentRender,
  // rightContentRender,
  // collapsedButtonRender,
  // footerRender,
  // pageTitleRender,
  // menuRender,
  // postMenuData,
  // menuItemRender,
  // subMenuItemRender,
  // menuDataRender,
  // breadcrumbRender,
  // route,
  // disableMobile,
  // links,
  // menuProps,
};

export default layout;
```

```javascript
// src/app.tsx
import React from "react";
// https://umijs.org/zh-CN/plugins/plugin-layout#运行时配置
interface ILayout extends Omit<BasicLayoutProps, "onError"> {
  logout: () => void;
  rightRender: (initialState: any) => React.ReactNode;
  onError: (error: Error, info: any) => void;
  ErrorComponent: (error: Error) => React.ReactElement<any>;
}

export const layout: ILayout = {
  logout: () => {},

  rightRender: (initialState: any) => {
    return <RightContent {...initialState} />;
  },

  // 菜单下方放置超链接
  links: [
    <a href="https://www.aliyun.com/" target="_blank" rel="noopener noreferrer">
      <AliyunOutlined />
       <span>阿里云</span>
    </a>,
    <a href="https://github.com/" target="_blank" rel="noopener noreferrer">
      <GithubOutlined />
       <span>Github</span>
    </a>,
    <a href="https://codesandbox.io/" target="_blank" rel="noopener noreferrer">
      <CodeSandboxOutlined />
       <span>CodeSandbox</span>
    </a>,
  ],

  footerRender: (props) => <GlobalFooter {...props} />,

  onError: (error, info) => {
    console.log("进入", "/src/app.tsx:layout:onError()", error, info);
    console.log("离开", "/src/app.tsx:layout:onError()", error, info);
  },

  ErrorComponent: (error) => {
    console.log("进入", "/src/app.tsx:layout:ErrorComponent()", error);
    console.log("离开", "/src/app.tsx:layout:ErrorComponent()", error);
    return <div />;
  },
};
```

# 路由与菜单

路由基本上与之前没什么变化，只是多了[几个属性](https://umijs.org/zh-CN/plugins/plugin-layout#%E6%89%A9%E5%B1%95%E7%9A%84%E8%B7%AF%E7%94%B1%E9%85%8D%E7%BD%AE)，关于图标我要说一下，[官方文档](https://umijs.org/zh-CN/plugins/plugin-layout#menu)上说是 antdv4 图标名去除后缀（outlined）并小写，但是我这里需要大写才能生效。

```javascript
// config/layout.config.ts
import { IBestAFSRoute } from "@umijs/plugin-layout";

const routes: IBestAFSRoute[] = [
  {
    name: "home",
    path: "/",
    component: "@/pages",
    menu: { name: "首页", icon: "Home" },
    layout: {
      hideMenu: true, // 隐藏菜单
      hideNav: true, // 隐藏页头
      hideFooter: true, // 隐藏页脚
    },
    hideInMenu: true,
  },
  {
    name: "dashboard",
    path: "dashboard",
    component: "@/pages/dashboard",
    menu: { name: "仪表板", icon: "Dashboard" },
    routes: [
      {
        name: "analysis",
        path: "analysis",
        component: "@/pages/dashboard/analysis",
        menu: { name: "分析页", icon: "Audit" },
      },
      {
        name: "monitor",
        path: "monitor",
        component: "@/pages/dashboard/monitor",
        menu: { name: "监控页", icon: "Monitor" },
      },
      {
        name: "workplace",
        path: "workplace",
        component: "@/pages/dashboard/workplace",
        menu: { name: "工作台", icon: "Desktop" },
      },
    ],
  },
];
```

# 性能优化

- 配置中开启 dynamicImport，打包后会按需加载，

```javascript
// config/config.ts
import { defineConfig } from "umi";

export default defineConfig({
  // https://umijs.org/zh-CN/config#dynamicimport
  dynamicImport: {
    loading: "@/components/PageLoading",
  },
});
```

- 还可以通过配置 splitChunks + chunk 的方式做代码分割，

```javascript
// config/config.ts
import { defineConfig } from "umi";
import chainWebpack from "./webpack.config";

export default defineConfig({
  chainWebpack,
  chunks: ["react", "utils", "charts", "vendors", "umi"],
});
```

```javascript
// config/webpack.config.ts
const chainWebpack: any = (config: any, { webpack }: any) => {
  // 这里只能这么写，config.merge的方式有问题
  config.optimization.splitChunks({
    // chunks: 'all',
    // minSize: 30000,
    // minChunks: 3,
    // automaticNameDelimiter: '.',
    cacheGroups: {
      // 组件库相关
      react: {
        name: "react",
        chunks: "all",
        test: /[\\/]node_modules[\\/](react|react-dom|react-router|react-router-dom|moment|antd|@ant-design)[\\/]/,
        priority: 12,
      },
      // 工具库相关
      utils: {
        name: "utils",
        chunks: "all",
        test: /[\\/]node_modules[\\/](lodash|ramda)[\\/]/,
        priority: 11,
      },
      // 图表库相关
      charts: {
        name: "charts",
        chunks: "all",
        test: /[\\/]node_modules[\\/](echarts|bizcharts|@antv)[\\/]/,
        priority: 11,
      },
      vendors: {
        name: "vendors",
        chunks: "all",
        test: /[\\/]node_modules[\\/]/,
        priority: 10,
      },
    },
  });
};

export default chainWebpack;
```

- 也可以使用 externals + scripts + styles 属性将三方类库通过 cdn 引入。

```javascript
// config/config.ts
import { defineConfig } from "umi";

export default defineConfig({
  // https://umijs.org/zh-CN/config#externals
  // https://umijs.org/zh-CN/guide/boost-compile-speed#配置-externals
  // prettier-ignore
  externals: {
    'react': 'React',
    'react-dom': 'ReactDOM',
    'moment': 'moment',
    'lodash': '_',
    'ramda': 'R',
    'antd': 'antd',
  },

  // 引入被 external 库的 scripts
  scripts:
    process.env.NODE_ENV === "development"
      ? [
          "https://cdn.jsdelivr.net/npm/react@16.13.1/umd/react.development.js",
          "https://cdn.jsdelivr.net/npm/react-dom@16.13.1/umd/react-dom.development.js",
          "https://cdn.jsdelivr.net/npm/moment@2.27.0/moment.js",
          "https://cdn.jsdelivr.net/npm/lodash@4.17.19/lodash.js",
          "https://cdn.jsdelivr.net/npm/ramda@0.27.1/dist/ramda.js",
          "https://cdn.jsdelivr.net/npm/antd@4.5.2/dist/antd.js",
        ]
      : [
          "https://cdn.jsdelivr.net/npm/react@16.13.1/umd/react.development.js",
          "https://cdn.jsdelivr.net/npm/react-dom@16.13.1/umd/react-dom.production.min.js",
          "https://cdn.jsdelivr.net/npm/moment@2.27.0/moment.min.js",
          "https://cdn.jsdelivr.net/npm/lodash@4.17.19/lodash.min.js",
          "https://cdn.jsdelivr.net/npm/ramda@0.27.1/dist/ramda.min.js",
          "https://cdn.jsdelivr.net/npm/antd@4.5.2/dist/antd.min.js",
        ],

  styles:
    process.env.NODE_ENV === "development"
      ? ["https://cdn.jsdelivr.net/npm/antd@4.5.2/dist/antd.css"]
      : ["https://cdn.jsdelivr.net/npm/antd@4.5.2/dist/antd.min.css"],
});
```

这里要说一下，如果 antd 也用 cdn 方引入，则代码里涉及到 less 变量的要先引入如下内容：

```less
@import "~antd/lib/style/themes/default.less";

.other-style {
}
```

我这里遇到一个问题就是 antd 怎么弄都会打包进去，翻看 issues 说是收到 babel-plugin-import 影响，
但是我根本没开启 antd，不知道为什么还是不行。

# 权限

权限这块比之前简单，但是我遇到一个问题，即使 canAccess 是 false，菜单中还是会显示，只是不能访问（显示 404），
而且会影响国际化，切换语言不会变，这块我尝试着阅读 pro-layout 源码，没找到原因，可能是版本问题，等更新吧

# 插件

新版集成了很多插件，有些需要在配置文件 config.ts 里手动开启，有些存在某个文件就默认开启，所以要确保文件存在，并且内容正确，否则引入会失败。比如说 plugin-dva，plugin-access 等，如果发现引入报错，可以查看一下/src/.umi 目录下的源码，看下是不是插件不存在，这时候就要排查一下了。

# 未完待续
