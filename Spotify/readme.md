## 🎯 项目架构总结文档（正式报告风格）

### 📌 项目技术栈概览
| 分类        | 技术/库                         |
|-------------|---------------------------------|
| 架构模式     | MVVM + Repository + DI         |
| UI 构建     | Jetpack Compose + Fragment + Navigation Component |
| 状态管理     | ViewModel + StateFlow + Flow   |
| 播放器引擎   | ExoPlayer                       |
| 网络请求     | Retrofit + GsonConverterFactory |
| 数据缓存     | Room + Flow                     |
| 依赖注入     | Dagger Hilt                     |
| 图片加载     | Coil                            |
| 测试支持     | MockServer (10.0.2.2)           |

---

## 🧾 一、正式报告风格（项目文档）

### 🧱 架构总览图
```
MainActivity
 └── BottomNavigationView + NavHostFragment
       ├── HomeFragment → HomeScreen (Compose)
       ├── FavoriteFragment → FavoriteScreen (Compose)
       └── PlaylistFragment → PlaylistScreen (Compose)

PlayerBar（ComposeView）
 └── PlayerViewModel + ExoPlayer（全局控制器）

每个 Fragment 对应自己的 ViewModel 和 Repository：
Fragment → ViewModel → Repository → Retrofit / Room
```

### 📂 分层结构与职责
- Application：初始化 Hilt 注入系统（MainApplication）
- Activity：UI 宿主 + 播放器承载（MainActivity）
- Fragment：加载 Compose UI + 路由跳转（Home/Favorite/Playlist）
- ViewModel：状态管理与 Repository 调用
- Repository：连接 Retrofit / Room 数据源
- Data Layer：Retrofit 接口、Room DAO、ExoPlayer 播放器

### 🎧 播放器模块设计
- PlayerViewModel 控制播放器逻辑，提供 PlayerUiState 给 PlayerBar 和 Playlist 页面消费
- 使用 StateFlow 推送状态，包含播放进度、播放状态、当前曲目信息等

---

## 🎤 二、面试口语化风格

“我们这个项目用的是 MVVM 架构，底层数据都封装在 Repository 层，ViewModel 负责状态管理，Compose UI 响应式地展示内容。”

🧱 架构拆解讲法：
- 一进来是 MainActivity，承载导航组件 + 全局 PlayerBar
- 每个页面是一个 Fragment，但 UI 是 Compose 写的，Fragment 只负责挂载
- Fragment 对应一个 ViewModel，ViewModel 通过 Repository 拿数据，数据来源是 Retrofit 或 Room
- 播放器用的是 ExoPlayer，由 Hilt 全局注入，统一由 PlayerViewModel 控制

📦 状态管理：
- 全部用 StateFlow 管理 UI 状态，Compose 用 collectAsState 自动绑定，用户体验非常顺滑

🎧 播放体验：
- 点击歌曲后，会调用 PlayerViewModel 的 `load()` 和 `play()`，同时底部 PlayerBar 会响应播放状态，当前播放项也会在列表中高亮

📈 拓展性亮点：
- 网络层用 Retrofit 封装，MockServer 可测试
- 收藏操作落地到 Room，Flow 支持自动更新收藏页
- 播放器状态全局唯一，UI 层完全解耦

🧠 面试时可以补充：
> 比如问“状态同步怎么做的”、“能否离线播放”、“Room 和网络怎么组合”等等，都能切到 ViewModel + Flow 的设计。

---

## 🧠 三、精炼速查版（结构总览）

### 🧩 架构核心路径
```
Activity → Fragment → Compose UI
         ↓
      ViewModel (StateFlow)
         ↓
     Repository (注入)
         ↓
Retrofit / Room / ExoPlayer
```

### 💡 模块说明
| 层级        | 核心组件                        | 功能概要                         |
|-------------|----------------------------------|----------------------------------|
| Application | MainApplication                  | 初始化 Dagger Hilt               |
| Activity    | MainActivity                     | 宿主容器 + 底部播放器             |
| UI          | Fragment + Compose Screen        | 三大页面：Home / Favorite / Playlist |
| ViewModel   | HomeViewModel 等                 | 管理 StateFlow，状态驱动 UI       |
| Repository  | HomeRepository 等                | 封装数据访问逻辑（网络/本地）     |
| 数据层      | Retrofit, Room, ExoPlayer        | 数据源 & 播放引擎                 |

### 📦 技术栈一览
- UI：Compose + Fragment
- 状态：StateFlow + ViewModel
- 网络：Retrofit + MockServer
- 本地：Room + Flow
- 播放器：ExoPlayer + PlayerViewModel
- 注入：Dagger Hilt 全局管理

### 🚀 亮点速览
- 🔁 UI 响应式全自动刷新（StateFlow + Compose）
- 🎧 播放器全局控制 + 播放状态同步
- 💾 Room + Flow 实现收藏实时更新
- 🧩 层次分明，组件解耦，Mock 易测
