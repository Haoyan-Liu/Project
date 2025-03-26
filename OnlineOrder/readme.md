## 📦 OnlineOrder Project Summary (Spring Boot + React)

### 🔧 Tech Stack
`Spring Boot`, `Spring Data JDBC`, `Spring Security`, `PostgreSQL`, `React.js`, `Ant Design`, `AWS RDS`, `AWS App Runner`

## 🔍 分层总结：前后端模块与技术栈职责

### 🖥️ 后端（Spring Boot）
| 模块/技术         | 功能描述 |
|------------------|----------|
| **Spring Boot**  | 提供项目入口、自动配置与 REST 接口开发框架 |
| **Spring MVC**   | 实现 Controller → Service → Repository 层级调用 |
| **Spring Security** | 管理用户登录验证与密码加密（使用 session-based 认证） |
| **Spring Data JDBC** | 持久化数据（Customer、Cart、MenuItem 等），简化数据库访问逻辑 |
| **PostgreSQL**   | 存储用户、菜单、订单等核心业务数据 |
| **AWS RDS**      | 云端部署数据库服务，保障持久性与可扩展性 |
| **App Runner**   | 无服务器部署平台，实现后端容器化部署与自动扩展 |

### 💻 前端（React + Ant Design）
| 模块/技术        | 功能描述 |
|------------------|----------|
| **React.js**     | 构建前端 SPA 应用，使用函数组件与 Hook 处理状态逻辑 |
| **Ant Design**   | 实现页面布局（Layout）、表单（Form）、抽屉（Drawer）与提示反馈（message）等交互组件 |
| **LoginForm / SignupForm** | 支持用户注册登录并与后端接口对接 |
| **FoodList**     | 展示餐厅菜单项，可添加至购物车 |
| **MyCart**       | 购物车模块，支持实时查看与结账操作 |
| **axios / fetch**| 实现与 Spring Boot 后端的异步 API 调用 |
