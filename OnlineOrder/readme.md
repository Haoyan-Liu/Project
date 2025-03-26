## 🍽 OnlineOrder - Full Stack Food Ordering System

### OnlineOrder: A Spring Boot based online food ordering system

- Developed RESTful APIs using Spring Boot to support registration, menu retrieval, cart operations, and order checkout.
- Utilized Spring Data JDBC with PostgreSQL for database access, deployed on AWS RDS.
- Implemented session-based authentication using Spring Security, including encrypted credential storage.
- Structured the backend into layered architecture (Controller → Service → Repository) for modularity and testability.
- Built a responsive frontend using ReactJS and Ant Design, enabling real-time cart updates and user interactions.
- Deployed the backend using Docker on AWS App Runner, enabling horizontal scalability and cloud CI/CD.

---

## 🧠 一、精炼速查版（结构总览）

### 🧩 架构核心路径
```
Frontend (React)
  → Component (LoginForm / FoodList / MyCart)
    → Axios / Fetch → Spring Boot API
      → Controller → Service → Repository → PostgreSQL
```

### 💡 模块说明
| 层级       | 核心组件                     | 功能概要                                           |
|------------|------------------------------|----------------------------------------------------|
| Frontend   | React + Ant Design           | 构建 SPA，用户交互 + 表单提交 + 弹窗购物车             |
| API 调用   | axios / fetch                | 向 Spring Boot 发起 REST 请求                     |
| Controller | MenuController 等             | 接收前端请求并分发到业务逻辑层                     |
| Service    | CartService / CustomerService | 处理核心业务逻辑（加购物车、结账、注册、登录）        |
| Repository | Spring Data JDBC Repository  | 执行数据库读写（使用命名函数或 @Query）             |
| 数据库      | PostgreSQL + AWS RDS         | 持久化用户、订单、菜单、购物车信息                   |

### 📦 技术栈一览
- 前端：React.js + Ant Design + Drawer + Form
- 状态管理：useState / useEffect（轻量）
- 后端：Spring Boot + Spring MVC + JDBC + Security
- 鉴权：Spring Security + Session + PasswordEncoder
- 数据库：PostgreSQL + Spring Data JDBC
- 部署：AWS RDS + AWS App Runner

### 🚀 项目亮点速览
- 🔐 完整的注册登录认证流程（Spring Security）
- 🛒 支持实时购物车管理 + 弹窗 UI + 多菜品处理
- 🧩 后端职责分层清晰（Controller → Service → Repository）
- ☁️ 全项目部署于 AWS，支持 CI/CD 与自动扩缩容
- 🧪 Mock 数据初始化（DevRunner）助力测试演示

---

## 🎤 二、面试口语化风格

“这个项目是一个基于 Spring Boot 的全栈在线点餐系统。我们将后端按照 MVC 架构解耦，使用 Spring Security 管理登录流程。前端则用 React 和 Ant Design 构建 SPA 页面，包括菜单浏览和购物车功能。”

🧱 架构讲解：
- 前端：SPA 页面用 React 构建，使用 Ant Design 实现登录表单与购物车弹窗。
- 后端：Controller 接受请求，交由 Service 层处理业务逻辑，Service 操作 Repository 实现数据持久化。
- 安全：注册后，用户使用 Spring Security 登录，后端维护会话信息。
- 数据：所有数据存储于 PostgreSQL，并通过 JDBC 访问。
- 部署：服务打包后部署至 AWS App Runner，数据库托管于 AWS RDS。

🧠 面试时可拓展：
- 为什么选择 JDBC 而不是 JPA？（轻量 + 明确 SQL 控制）
- 如何保证购物车更新原子性？（使用 @Transactional 注解）
- 如何支持后续加前端状态管理（如 Redux）或支付功能？

---

## 🧾 三、正式报告风格（项目文档）

### 🧱 架构总览图
```
OnlineOrderApplication
 ├── SecurityFilterChain
 └── AppConfig
       └── UserDetailsManager / PasswordEncoder

🔁 用户请求流：
Browser (React)
 └── LoginForm / FoodList / MyCart
      ↓ REST API
Controller
 └── Service
       └── Repository
             └── PostgreSQL (AWS RDS)
```

### 📂 分层结构与职责
- **AppConfig**：初始化核心 Bean，包括密码加密器与用户管理器
- **Controller**：接收前端请求，如 `/signup`、`/cart/checkout` 等
- **Service**：封装业务逻辑，如注册自动建购物车、购物车加菜判断是否重复
- **Repository**：使用 Spring Data JDBC 提供基本的 CRUD 操作（如 `findByEmail`, `deleteByCartId`）
- **实体结构**：Customer、Cart、OrderItem、MenuItem、Restaurant 等五张核心表
- **DTO 层**：封装返回对象，前后端解耦

### 🖥️ 前端模块
| 组件名       | 功能描述                                |
|--------------|-----------------------------------------|
| `LoginForm`  | 用户登录功能，成功后更新父组件状态（authed） |
| `SignupForm` | 弹窗注册表单，连接后端 `/signup` 接口       |
| `FoodList`   | 展示所有餐厅 + 菜单项                     |
| `MyCart`     | 抽屉组件展示当前用户购物车，支持 checkout   |

---

✅ 如需导出完整 Markdown / PDF / Word，请随时告知格式！

