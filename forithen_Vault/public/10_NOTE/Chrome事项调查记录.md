# 事项总类
	两大类
1. 画面表示的差分 例如画面上的表格的layout崩了
2. 没有报错的情况下出现白画面
# 前端调查基础
前端调查不是为了“写JS”，而是为了回答这三个问题：
1. 点击/打开页面时，浏览器到底发了什么请求？（Network）
2. 浏览器收到了什么响应？（Response / 状态码）
3. 浏览器为什么没把画面渲染出来？（Console / 资源加载 / 跳转链）
## DevTools 三个面板
### A. Network（最重要）
看请求、状态码、是否302/500、响应内容、耗时。
#### 状态码
##### 1️⃣ 200 系列 —— 成功

###### 200 OK
👉 请求成功，服务器正常返回
但要注意
> 200 不代表没问题
比如：
- 返回的是错误页HTML
- 返回的是空页面
- 返回的不是你预期的数据
所以一定要看 **Response 内容**。

###### 2️⃣ 300 系列 —— 重定向（非常重要）
**302 Found（最常见）**
表示：
> 服务器让浏览器跳转到另一个URL

常见情况：
- 未登录 → 跳 login
- 异常 → 跳 error 页面
- 权限不足 → 跳错误页
你看到白屏时，302是非常关键线索。
在 DevTools 里看：
Network → 点那条请求 → Headers → 看：
Status Code: 302  
Location: /login.xhtml

###### 3️⃣ 400 系列 —— 客户端错误
**401 Unauthorized**
未认证（没登录/Session失效）

**403 Forbidden**
权限不足

**404 Not Found**
资源路径错误（JS/CSS丢失常见）
这些都可能导致白屏。

###### 4️⃣ 500 系列 —— 服务器错误（你遇到的OOM）
**500 Internal Server Error**
说明：
> 后端代码抛异常了

此时：
- 必须去看 server.log
- Response 里通常有错误HTML或异常信息
### B. Console（第二重要）
看 JS error、Blocked（CSP/Mixed content）、cookie警告等。
### C. Elements（辅助）
确认某个DOM是否存在、是否真的“全白”（body里有没有东西）。
## Preserve log 是什么
**Preserve log = 保留网络日志**。
默认情况下，如果发生跳转（302）或页面刷新，Network 面板会把之前的请求清掉。  
这样你就看不到“白屏前发生了什么”。
白屏经常是：
- 302 → 又302 → 跳到error或login
- 或 500 → 页面被替换成空白
- 或某个JS加载失败 → 后续脚本没执行
不开 Preserve log，你只看到最后的空白页面，前因都没了。
✅ 所以：**查白屏必须开 Preserve log**。
## 白屏调查 SOP
下面这个顺序是“最省时间、信息量最大”的。

### Step 1：准备（每次调查都先做）
1. 打开 Chrome DevTools（F12）
2. Network：
    - ✅ 勾选 **Preserve log**
    - ✅ 勾选 **Disable cache**
3. Console：
    - 保持打开
然后再开始操作复现。

### Step 2：白屏发生瞬间
不要急着刷新页面。
#### 2.1 先看 Console 有没有红字
- `Uncaught TypeError...`
- `ReferenceError...`
- `Blocked by...`（CSP / Mixed content / CORS）
- cookie相关警告（SameSite等）
👉 有红字就先截图/复制。

### Step 3：看 Network（核心）
在 Network 上方过滤器，先选：
- **Doc**（document）
- **JS**
- **CSS**
#### 3.1 先看 Doc（页面本体请求）
找最上面那条 document 请求，看：
- 状态码：200 / 302 / 401 / 403 / 500
- 点开看 Headers：
    - **Location**（如果是302）
- 点开看 Response：
    - 是不是HTML？
    - 是不是错误页？
**判断规则：**
- 如果是 **500** → 先去看后端日志（你已经碰到过OOM）
- 如果是 **302** → 追跳转链（Preserve log 的价值在这里）
- 如果是 **200** 但白 → 多为资源/JS问题
#### 3.2 再看 JS/CSS 是否有 404/blocked
如果 JS/CSS 中有任何：
- 404
- (blocked)
- net::ERR_...
那很可能就是白屏根因（脚本没加载/样式缺失/被安全策略拦了）。

### Step 4：用“一眼判定”把问题归类
你只要按下面四类归就行：
#### 类型A：JS致命错误（前端）
- Console有Uncaught error
- Network可能正常  
    → 去定位是哪一个JS文件/哪一行
#### 类型B：资源加载失败（前端/构建/路径）
- JS/CSS 404 或 blocked  
    → 修路径、CSP、Mixed Content、缓存
#### 类型C：跳转链/认证问题（前端+环境）
- Network里出现 302/401/403  
    → 看 cookie 是否带上、Location去哪、是否跳login/error
#### 类型D：后端错误（后端/性能/内存）
- 500 / 超时 / pending很久  
    → 看 server.log、OOM、SQL等待等

# 事项1 大类调查

# 事项2 大类调查
## 调查的方针
### 0.先做两件事（为了可复现与对比）
1. **同一操作在 Edge vs Chrome 对比**
- Edge正常、Chrome白屏 → 优先按“浏览器差异/前端”路径查
- 两个都白屏 → 优先按“后端/环境/数据”路径查
1. **确认是“全白”还是“局部区域白”**
- 局部白（某个panel没渲染）→ 多为 JSF Ajax/DOM更新问题
- 全白（整个页面空白）→ 多为 JS报错/资源加载失败/500错误
### 1.第一优先：浏览器控制台（Console）

**目的：10秒拿到最直接线索。**
看三类：
#### A) JavaScript Error
- `Uncaught TypeError...`
- `Cannot read properties of null`
- `xxx is not defined`
→ 通常是 **DOM找不到/JS执行顺序/ID变化**（JSF迁移后常见）
#### B) Security / Cookie / CSP / Mixed Content
- `Blocked by CORS policy`
- `Mixed Content blocked`
- `SameSite` / cookie相关警告
→ 通常是 **Chrome更严格导致的阻断**
#### C) JSF相关
- 看到 `ViewExpiredException` 相关提示（有时在响应里）

### 2.第二优先：Network 看“有没有请求、返回什么”
**这是白屏定位的核心。**
按这几步看：
#### A) 有没有请求发出去？
- 点击按钮后 Network 完全没动  
    → 多为 **事件没绑定 / JS分支没执行 / onclick被阻断**
#### B) 有请求但返回 4xx/5xx？
- 500/404  
    → 先看响应内容（Response）通常直接写原因
#### C) 返回成功但画面没更新？
重点看：
- Response 里有没有 `<partial-response>`（JSF Ajax）
- Header 里有没有 `Faces-Request: partial/ajax`
如果有 `<partial-response>` 但画面不更新：  
→ 多为 **render目标ID不存在 / DOM被替换失败 / JS异常中断**

### 3. 第三优先：判断是不是“资源加载失败导致白屏”
在 Network 里过滤：
- JS
- CSS
- Font

看是否有：
- 404（路径错）
- 302→登录页（Session掉了）
- 被阻断（blocked）
**典型场景：**  
JSF迁移后资源路径变了，Chrome缓存/策略不同，更容易暴露。

### 4. 第四优先：JSF 特有路径（白屏最常见根因之一）
如果你确认是 JSF：
#### A) ViewState 是否正常
Network里找请求参数/表单里：
- `javax.faces.ViewState`
如果：
- ViewState缺失/为空/过期
- 请求返回 `ViewExpiredException`
→ 方向：**Session/Cookie/SameSite/超时/多Tab**
#### B) render/update 的目标是否存在
在 `<partial-response>` 里会有：
```
<update id="form:xxx">...</update>
```
然后你在 Elements 里搜：
- `id="form:xxx"`
如果页面里没有这个id：  
→ **render指定错 / 组件树变化 / 命名容器导致id变化**

### 5. 第五优先：后端日志（应用日志优先于DB）
如果 Network 显示 500 或 Response 有异常堆栈：
优先看：
- JBoss/WildFly server.log
- 应用日志（业务异常/NullPointer/SQL异常）
因为白屏很多时候是：
- 后端抛异常 → 前端拿到错误页/空响应 → 画面白

### 6. 第六优先：数据差异/环境差异验证
当你已经确认：
- 前端没明显JS错误
- 请求也正常
- 但只在regression某些数据下白屏
那就做：
#### A) 同一请求参数/同一用户/同一数据在本地跑对比
- 如果本地正常、regression异常 → 环境/数据差异
- 如果本地也异常 → 代码缺陷
#### B) DB层是否发生锁等待/超时
白屏有时是“请求一直没回来”。
Network里看该请求：
- Pending很久
- TTFB很长
再看后端线程/DB等待（必要时）：
- SQL执行时间
- lock等待（TM/TX）

### 7. 排查顺序总结
**白画面调査は以下の順で実施する：**
1. Edge/Chromeの再現性比較（ブラウザ差異か切り分け）
2. ConsoleでJS/セキュリティエラー有無確認
3. Networkでリクエスト有無・ステータス・レスポンス内容確認
4. JSFの場合、partial-response・ViewState・render対象IDの整合性確認
5. 5xx/異常時はJBossログで例外確認（アプリ層優先）
6. 追加でデータ差異・性能/待ち（DB）要因を確認

## 实际情况
### 背景
本次的白画面的出现基本上都是 画面初期表示 & 默认条件检索的时候出的问题
作业的流程来说的话如下
1. 打键 确认问题
2. local环境调查
但是目前在local环境中大部分的白画面都再现不了，Chrome的版本和Regression环境保持了一致。
补足：
1.Edge同时对照打键并没有出问题。
2.目前无法用regression环境
3.白画面时是全白 并非局部Ajax的状态
#### 全画面白屏最常见根因（Edge正常、Chrome异常）
既然是**全画面**，优先考虑这三类（按概率）：
##### A. JS/CSS等静态资源加载失败（或被Chrome阻断）
- Chrome更严格的安全策略（Mixed Content / CSP / 不安全资源）
- 缓存/Service Worker（如果有）导致加载异常
- 资源路径在某些条件下生成不同（框架迁移后常见）
**表现**：页面框架都出不来，直接白；Console通常会有红字（404、blocked、CSP等）。
##### B. 初期表示时发生跳转/重定向/认证失败，但被前端处理成白
- Chrome Cookie策略（SameSite/Secure）导致Session拿不到
- 结果：被重定向到login或error页面，但前端渲染失败或被脚本覆盖
**表现**：Network里会看到302/401/403；但你现在看不到regression，所以只能在local模拟“Cookie更严格”的条件。
##### C. 初期脚本执行差异导致致命错误
- DOM未就绪就访问元素：`Cannot read properties of null`
- 某个仅在Chrome触发的分支执行（比如浏览器判定、UA差异）
- JSF迁移后某些全局脚本依赖结构改变
**表现**：Console出现Uncaught error，页面不渲染。

> 你说“不是Ajax”，其实更像 A/B/C 这种**“加载阶段致命失败”**。
### 背景补充
我本地尝试复现的时候 出现过
以下事项
1. 检索的时候 数据量大？（究竟是不是数据量大 存疑）导致Java OutOfMemory，返回500
2. 重定向 302，到error页面。但是白画面。（但是不是目标页面出的问题，是随手操作的时候出现的，不能稳定复现）
