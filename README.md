## 目录结构 (Directory Structure)

Plaintext

```
.
├── docs/               # 设计文档与架构图 (Draw.io/PDF)
├── models/             # Simulink 模型 (.slx) 及配套脚本 (.m, .mat, .capr)
├── tests/              # 测试用例与仿真数据
└── README.md           # 项目说明
```

## 系统架构 (System Architecture)

> 请参考 `docs/architecture/` 目录下的详细设计图。

### 1. 核心功能交互流程
*(在此处插入之前绘制的流程图图片，建议命名为 vcu_flow.png)*
![功能交互流程](./docs/images/vcu_flow.png)

### 2. 模块输入输出定义
*(在此处插入架构参考图，建议命名为 vcu_architecture.png)*
![架构输入输出](./docs/images/vcu_architecture.png)

---

## 功能开发清单

根据《二期功能开发进展》，请认领以下模块并提交代码/文档：

### 驱动控制 (Longitudinal Control)
- [ ] **预见性巡航控制 (Predictive Cruise)**
    - [ ] 坡度/阻力估算 
    - [ ] 预见性目标加速度计算 (PID + 规则)
- [ ] **双桥驱动分配 (Dual-Bridge Torque Allocation)**
    - [ ] 动态轴荷计算
    - [ ] 基于效率MAP的转矩分配 
- [ ] **单双桥切换策略 (Bridge Switching)**
    - [ ] 驾驶意图与工况识别 [cite: 79, 100]
    - [ ] 滞回策略防止频繁切换
    - [ ] 
### 制动控制 (Braking Control)
- [ ] **制动力分配 (Braking Distribution)**
    - [ ] 的前后轴力矩分配
    - [ ] ECE制动法规线校核 
- [ ] **主挂解耦 (Trailer Decoupling)**
    - [ ] 挂车制动力转移计算 
    - [ ] 牵引车电机制动回馈优化

### 横向稳定性 (Lateral Stability)
- [ ] **驱制动协同控制**
    - [ ] 上层：横摆角速度PID控制器
    - [ ] 下层：电机与EBS协同转矩分配

---
为确保多人协作时模型的可运行性和架构的一致性，请严格遵守以下两点要求：

### 1. 架构与流程图维护
在开发过程中，如果因具体实现细节导致逻辑与原设计不符，或需要新增接口/状态：
* **必须同步更新架构图**：请修改 `docs/` 下对应的 draw.io 源文件。
* **完善细节**：根据你负责模块的实际情况，在流程图中补充具体的判断条件、参数定义或跳转逻辑。
* **提交变更**：架构图的修改需随代码一同提交。

### 2.功能包完整性
提交功能模块时，必须确保“**下载即运行**”。Pull Request 必须包含完整的工程文件包。

**必需包含的文件清单：**
* `*.slx` : Simulink 模型源文件
* `*.m` : 初始化脚本、参数定义脚本（Init/Config scripts）
* `*.mat` : 标定数据、Map表数据或测试输入数据
* `*.capr` / `*.prj` : 工程配置文件或相关工具链配置
* **其他依赖** : 任何让程序跑起来所必须的自定义文件

> **自测标准**：请在提交前，在一个干净的文件夹中尝试运行你的脚本和模型，确保不报错、不缺文件

---


为了保证多人协作的顺畅，请遵循以下 **Fork & Pull Request** 流程：

1. **Fork 本仓库**
   点击右上角的 `Fork` 按钮，将项目复制到你自己的 GitHub 账户。

2. **Clone 到本地**
   ```bash
   git clone [https://github.com/你的用户名/ProjectName.git](https://github.com/你的用户名/ProjectName.git)

   1. **创建开发分支 (Branch)** 请务必在分支上进行开发，不要直接修改 main 分支。 *命名规范：`feat/模块名` 或 `fix/bug描述`*

   Bash

   ```
   git checkout -b feat/sliding_mode_control
   ```

2. **开发与打包**

   - 编写代码/模型。
   - **更新架构图**（如有变动）。
   - **整理所有依赖文件**（.slx, .m, .mat, .capr等）。

3. **提交更改 (Commit)** 提交信息请简要描述修改内容。

   Bash

   ```
   git add .
   git commit -m "feat: 完成滑模控制前后轴分配算法实现，并更新对应架构图"
   ```

4. **推送分支 (Push)**

   Bash

   ```
   git push origin feat/sliding_mode_control
   ```

5. **发起 Pull Request (PR)** 回到原仓库页面，点击 `New Pull Request`，请求将你的分支合并到 `main` 分支。请在 PR 描述中说明你完成了哪个功能点。

------


## 注意事项

- 修改模型前请先拉取最新代码：`git pull origin main`
- 所有新增算法模块需包含详细的输入输出注释。


