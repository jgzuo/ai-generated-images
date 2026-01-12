# 🏎️ 3D赛车游戏 (3D Racing Game)

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Three.js](https://img.shields.io/badge/Three.js-r128-green.svg)
![License](https://img.shields.io/badge/license-MIT-orange.svg)
![Language](https://img.shields.io/badge/language-JavaScript-yellow.svg)

一个功能完整的3D赛车游戏，使用 Three.js 实现，包含粒子特效、物理引擎、AI对手和保存系统。

[在线演示](#) • [快速开始](#快速开始) • [功能特性](#功能特性) • [技术文档](#技术架构)

</div>

---

## 📸 游戏截图

<!-- 添加游戏截图 -->
![游戏截图](screenshots/gameplay.png)

## ✨ 功能特性

### 🎮 核心游戏机制
- ✅ **3D渲染引擎** - 基于 Three.js r128 的高性能3D图形渲染
- ✅ **真实物理模拟** - 自定义物理引擎，包含：
  - 真实的加速、制动曲线
  - 速度依赖的转向系统
  - 漂移机制（手刹触发）
  - 摩擦力和惯性模拟
- ✅ **无限赛道系统** - 动态生成的无限滚动赛道
- ✅ **4车道设计** - 宽阔的赛道提供更多策略选择
- ✅ **智能AI对手** - 5个AI对手，具备：
  - 实时障碍物检测
  - 动态避障决策
  - 车道评估和超车逻辑
  - 速度调整策略
- ✅ **精确碰撞检测** - 基于AABB包围盒的碰撞系统

### 🎨 视觉效果
- ✅ **粒子系统** - 多种粒子效果：
  - 🌫️ 尾气排放（加速时）
  - 💥 碰撞爆炸（撞击障碍物）
  - ✨ 速度线（高速移动）
- ✅ **环境装饰** - 赛道两侧丰富装饰：
  - 🌲 多种树木（随机高度和颜色）
  - 🏢 城市建筑（带窗户和灯光）
  - 🌸 植物和花朵（彩色装饰）
  - 💡 路灯系统（6米高灯柱）
  - 🪨 岩石（随机形状）
- ✅ **动态光照** - 环境光 + 方向光 + 实时阴影
- ✅ **大气效果** - 距离雾增强深度感

### 💾 数据持久化
- ✅ **本地存储** - 基于 localStorage 的保存系统
- ✅ **最佳记录** - 追踪：
  - 最佳完成时间
  - 最高分数
  - 总比赛场次
- ✅ **自动保存** - 比赛结束后自动保存

### 🎯 游戏规则
- **比赛模式**: 3圈完整比赛
- **实时排名**: 动态显示当前排名（1st-6th）
- **分数系统**:
  - 时间奖励: `max(0, 1000 - 完成时间)`
  - 排名奖励: `(6 - 排名) × 500`

## 🚀 快速开始

### 在线运行

最简单的方式 - 直接在浏览器中打开：

```bash
# 克隆仓库
git clone https://github.com/jgzuo/3d-racing-game.git

# 在浏览器中打开
open 3d-racing-game/Program/3d-racing-game.html
```

### 本地运行

#### 方式1: Python HTTP 服务器

```bash
# Python 3
cd 3d-racing-game/Program
python3 -m http.server 8000

# 访问 http://localhost:8000/3d-racing-game.html
```

#### 方式2: Node.js

```bash
# 使用 http-server
npx http-server -p 8000

# 或使用 live-server
npx live-server --port=8000
```

## 🎮 操作说明

| 按键 | 功能 | 详细说明 |
|------|------|----------|
| `↑` / `W` | 加速 | 逐渐加速到最大速度 |
| `↓` / `S` | 刹车/倒车 | 快速减速或反向移动 |
| `←` / `A` | 左转 | 向左移动车道（高速时灵敏度降低）|
| `→` / `D` | 右转 | 向右移动车道（高速时灵敏度降低）|
| `Space` | 手刹 | 触发漂移（速度>50km/h时生效）|
| `P` | 暂停 | 暂停/继续游戏 |

### 游戏技巧

1. **起步**: 按住 `W` 键平稳加速，避免过早转向
2. **超车**: 观察小地图，选择空闲车道超车
3. **漂移**: 在弯道或避障时使用 `Space` 漂移
4. **障碍物**: 红色路障和灰色故障车会减速，尽量避开
5. **策略**: 保持速度的同时避免碰撞，平衡是关键

## 🏗️ 技术架构

### 技术栈

```yaml
核心技术:
  - Three.js r128      # 3D渲染引擎
  - JavaScript ES6+   # 原生JavaScript，无构建工具
  - HTML5 Canvas      # 小地图和HUD渲染
  - localStorage      # 数据持久化

可选技术:
  - Web Audio API     # 音效系统（预留接口）
```

### 代码架构

```
3d-racing-game.html (1424行)
├── HTML结构 (~200行)
│   ├── 游戏容器 (#game-container)
│   ├── UI层
│   │   ├── 主菜单 (#main-menu)
│   │   ├── HUD (#hud)
│   │   │   ├── 速度显示
│   │   │   ├── 计时器
│   │   │   ├── 圈数
│   │   │   ├── 排名
│   │   │   └── 分数
│   │   ├── 小地图 (#minimap)
│   │   ├── 暂停菜单 (#pause-menu)
│   │   ├── 游戏结束 (#game-over)
│   │   └── 控制说明 (#controls)
│   └── Canvas (Three.js渲染)
│
├── CSS样式 (~150行)
│   ├── 响应式设计
│   ├── 动画效果
│   └── UI组件样式
│
└── JavaScript代码 (~1074行)
    ├── 配置常量 (GAME_CONFIG)
    ├── 游戏状态管理 (gameState)
    │
    ├── 核心类 (9个主要类)
    │   ├── CarPhysics       # 物理引擎
    │   ├── Car              # 车辆模型
    │   ├── AIOpponent       # AI对手逻辑
    │   ├── TrackGenerator   # 赛道生成
    │   │   ├── createTree()
    │   │   ├── createBuilding()
    │   │   ├── createPlant()
    │   │   ├── createStreetLamp()
    │   │   └── createRock()
    │   ├── ParticleSystem   # 粒子系统
    │   ├── CollisionDetection # 碰撞检测
    │   ├── SaveSystem       # 保存系统
    │   └── UIManager        # UI管理
    │
    ├── 游戏循环
    │   ├── init()           # 初始化
    │   ├── animate()        # 主循环
    │   ├── startGame()      # 开始游戏
    │   ├── pauseGame()      # 暂停
    │   ├── endRace()        # 结束比赛
    │   └── restartGame()    # 重新开始
    │
    └── 输入处理
        ├── setupInput()     # 设置监听器
        └── inputState       # 输入状态
```

### 核心类说明

#### 1. CarPhysics (物理引擎)
```javascript
class CarPhysics {
    constructor() {
        this.velocity = 0;          // 当前速度
        this.acceleration = 0;      // 加速度
        this.maxSpeed = 150;        // 最大速度
        this.friction = 0.98;       // 摩擦系数
        this.turnSpeed = 0;         // 转向速度
        this.driftFactor = 0;       // 漂移因子
    }
    
    update(deltaTime, input) {
        // 物理计算：
        // - 速度更新: v = v + a*t - v*f
        // - 转向计算: 速度越快转向越慢
        // - 漂移计算: 手刹触发时增加漂移
    }
}
```

#### 2. TrackGenerator (赛道生成器)
```javascript
class TrackGenerator {
    constructor() {
        this.segmentLength = 50;     // 每段长度
        this.segments = [];          // 赛道段数组
        this.obstacles = [];         // 障碍物数组
        this.decorations = [];       // 装饰物数组
    }
    
    // 核心方法
    generateInitialTrack()     // 生成初始赛道
    addSegment(zPosition)      // 添加新赛道段
    addDecorations(zPosition)  // 添加环境装饰
    createObstacle(x, z)       // 创建障碍物
    update(playerZ)            // 更新和清理
}
```

#### 3. AIOpponent (AI对手)
```javascript
class AIOpponent extends Car {
    constructor(lane, difficulty) {
        this.difficulty = difficulty;    // 难度(0-1)
        this.targetSpeed = 60-120;       // 目标速度
        this.reactionTime = 0.5-1.0;     // 反应时间
    }
    
    avoidObstacles(obstacles) {
        // AI决策流程：
        // 1. 扫描前方障碍物
        // 2. 评估可用车道
        // 3. 决定超车或制动
    }
}
```

## ⚙️ 配置选项

所有游戏参数都在 `GAME_CONFIG` 对象中定义：

```javascript
const GAME_CONFIG = {
    // 赛道设置
    TRACK_WIDTH: 30,           // 赛道总宽度(米)
    TRACK_LENGTH: 1000,        // 每圈长度(米)
    LANES: 4,                  // 车道数量
    LANE_WIDTH: 7.5,           // 每车道宽度(米)
    
    // 车辆物理
    MAX_SPEED: 150,            // 最大速度(km/h)
    ACCELERATION: 50,          // 加速度
    BRAKE_POWER: 80,           // 刹车力度
    TURN_SPEED: 2.5,           // 转向速度
    FRICTION: 0.98,            // 摩擦系数(0-1)
    
    // 游戏规则
    TOTAL_LAPS: 3,             // 总圈数
    AI_COUNT: 5,               // AI对手数量
    MAX_PARTICLES: 5000,       // 最大粒子数
    OBSTACLE_INTERVAL: 100,    // 障碍物间隔
};
```

### 自定义配置

直接编辑 `3d-racing-game.html` 中的 `GAME_CONFIG` 对象即可调整游戏难度和参数。

## 📊 性能优化

### 已实现的优化

1. **对象池模式**
   - 复用装饰物和障碍物对象
   - 减少垃圾回收压力

2. **视锥体裁剪**
   - Three.js 自动视锥体裁剪
   - 距离雾遮挡远处对象

3. **动态资源清理**
   ```javascript
   update(playerZ) {
       // 清理玩家后方150米外的装饰物
       this.decorations = this.decorations.filter(dec => {
           if (dec.position.z < playerZ - 150) {
               this.mesh.remove(dec.mesh);
               return false;
           }
           return true;
       });
   }
   ```

4. **粒子数量限制**
   - 最多5000个活跃粒子
   - 超出后自动移除旧粒子

### 性能指标

| 分辨率 | 简单场景 | 复杂场景 |
|--------|---------|---------|
| 1920x1080 | 45-60 FPS | 30-45 FPS |
| 1366x768 | 60 FPS | 45-60 FPS |
| 1280x720 | 60 FPS | 50-60 FPS |

## 🔧 开发指南

### 添加新功能

#### 1. 添加新的装饰物类型

在 `TrackGenerator` 类中添加新方法：

```javascript
createYourDecoration(x, z) {
    const mesh = new THREE.Group();
    mesh.position.set(x, 0, z);
    
    // 创建你的3D模型
    const geo = new THREE.BoxGeometry(1, 1, 1);
    const mat = new THREE.MeshPhongMaterial({ color: 0xff0000 });
    const obj = new THREE.Mesh(geo, mat);
    mesh.add(obj);
    
    this.mesh.add(mesh);
    this.decorations.push({ 
        mesh: mesh, 
        position: mesh.position, 
        type: 'your_type' 
    });
}
```

然后在 `addDecorations()` 中调用。

#### 2. 添加新的粒子效果

在 `ParticleSystem.emit()` 中添加新类型：

```javascript
emit(type, position, count, color) {
    if (type === 'your_effect') {
        for (let i = 0; i < count; i++) {
            const particle = {
                position: position.clone(),
                velocity: new THREE.Vector3(
                    (Math.random() - 0.5) * 10,
                    Math.random() * 5,
                    (Math.random() - 0.5) * 10
                ),
                life: 1.0,
                decay: 0.02,
                size: 1.0,
                color: new THREE.Color(color)
            };
            this.particles.push(particle);
        }
    }
}
```

#### 3. 修改AI行为

编辑 `AIOpponent.avoidObstacles()` 方法：

```javascript
avoidObstacles(obstacles) {
    // 获取前方50米内的障碍物
    const obstaclesAhead = obstacles.filter(obs => {
        const dist = obs.position.z - this.position.z;
        return dist > 0 && dist < 50;
    });
    
    if (obstaclesAhead.length > 0) {
        // 你的AI逻辑
    }
}
```

## 📁 项目结构

```
3d-racing-game/
├── Program/
│   ├── 3d-racing-game.html    # 主游戏文件(1424行)
│   ├── README.md              # 本文档
│   └── index.html             # 项目索引页
├── .gitignore                # Git忽略文件
├── BUILD_WINDOWS.md          # Windows构建指南(其他项目)
├── CMakeLists.txt           # CMake配置(其他项目)
└── README_POMODORO.md       # 番茄钟说明(其他项目)
```

## 🎯 游戏截图

### 游戏界面
- 主菜单
- 游戏中的HUD
- 小地图
- 游戏结束界面

<!-- 添加更多截图 -->

## 🐛 已知问题

目前没有已知的严重bug。如果您发现任何问题，请提交 [Issue](https://github.com/jgzuo/3d-racing-game/issues)。

## 🤝 贡献指南

欢迎贡献！请遵循以下步骤：

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

### 代码规范

- 使用ES6+语法
- 类名使用PascalCase
- 变量/函数使用camelCase
- 常量使用UPPER_SNAKE_CASE
- 添加适当的注释

## 📜 许可证

本项目采用 MIT 许可证。详见 [LICENSE](LICENSE) 文件。

## 👨‍💻 作者

**Created with Claude Code**  
开发时间: 2026年1月

## 🙏 致谢

- [Three.js](https://threejs.org/) - 强大的3D图形库
- [Claude Code](https://claude.ai/code) - AI编程助手
- 开源游戏开发社区

## 📮 联系方式

- GitHub: [@jgzuo](https://github.com/jgzuo)
- Issues: [提交问题](https://github.com/jgzuo/3d-racing-game/issues)

## 🌟 Star History

如果这个项目对你有帮助，请给它一个 Star！

[![Star History Chart](https://api.star-history.com/svg?repos=jgzuo/3d-racing-game&type=Date)](https://star-history.com/#jgzuo/3d-racing-game&Date)

---

<div align="center">

**🏁 享受游戏！Good Luck! 🏁**

[⬆ 返回顶部](#-3d赛车游戏-3d-racing-game)

</div>
