# 全体顺序
1.背景与风险
2.打键范围策略指定方法
3.本次决策：为何选择全量
4.实际事项分类与调查流程 
  [[Chrome事项调查记录]]
5.conclude

## 背景与风险
## ■ 背景

本项目为在既存系统中新增 Chrome 浏览器支持。  
现行系统主要针对 Edge 进行适配，且同时期正在推进应用框架由 JS+Teeda 向 JSF 的迁移。

在多项目并行的背景下，本次 Chrome 追加不仅是浏览器适配问题，同时涉及前端框架结构变化及潜在回归风险。

### 1. 浏览器判定逻辑依赖风险（结构性风险）

系统现有前端代码中存在如下写法：
`if (!isEdge && !isFireFox) { ... }`
此类实现方式的本质问题为：
- 通过“排除法”进行浏览器判定
- 默认仅支持已知浏览器
- 未采用 feature detection（功能检测）方式

风险点：
- Chrome 作为新浏览器将被自动归类为“未知浏览器”
- 可能触发错误分支逻辑
- 部分功能可能被错误屏蔽或未执行
该风险属于：
> 代码结构层面的潜在不兼容风险

对应策略：
- 全量搜索浏览器判定代码
- 判断是否应改为 feature-based 判定
- 明确 Edge 专属逻辑与共通逻辑的分离
---

### 2. 框架迁移叠加风险（结构变更叠加）变量混杂风险（confounding variable）
本项目期间同时进行：
- JS + Teeda → JSF 迁移
该变更带来的影响包括：
- DOM结构变化
- 生命周期差异
- Ajax处理机制差异
- 组件ID生成规则变化

风险点：
- Chrome适配问题可能被误判为框架问题
- 框架变更导致的JavaScript依赖失效
- 事件绑定机制变化导致前端行为异常

该风险属于：

> 技术栈迁移叠加风险

对应策略：
- 明确“浏览器差异”与“框架差异”的边界
- 在 regression 环境中进行逐项对比验证
- 分离变量进行问题定位

---

### 3. Chromium系浏览器差异风险（运行时差异）

虽然 Edge 与 Chrome 同属 Chromium 内核，但：
- UA字符串不同
- 默认安全策略不同
- SameSite/Cookie处理差异
- 扩展机制差异
- 部分实验性API开启状态不同

风险点：
- Cookie传递异常
- Mixed Content警告
- CSP策略触发差异
- 缓存行为差异

该风险属于：
> 浏览器运行环境差异风险

对应策略：
- 使用 DevTools Network/Console 进行差分分析
- 比较响应Header与安全策略
- 重点关注认证流程与跨域请求
### 关于 JS+Teeda 和 JSF的对比

#### ① DOM结构变化
JSF生成的HTML与Teeda不同：
- id生成规则不同
- form嵌套结构不同
- component树结构不同
旧JS如果：
`document.getElementById("xxx")`
而JSF实际生成：
`formId:xxx`
就会失效。
这是结构机制。
#### ② 生命周期机制差异

JSF有：
- Restore View
- Apply Request Values
- Process Validations
- Update Model
- Invoke Application
- Render Response
Ajax局部刷新依赖生命周期。

如果JS在错误时机执行：
- DOM尚未更新
- 组件未绑定
就会出现“刷新异常”。
这是框架层机制。
#### ③ Ajax机制变化

JSF的：

`<f:ajax render="xxx"/>`
是基于：
- Partial Response
- ViewState
Chrome与Edge在：
- DOM ready
- 事件触发顺序
微小差异会影响局部更新。
##### Ajax是什么
Ajax = **Asynchronous JavaScript And XML**
非同期JS以及XML
但现在基本已经不是XML了，而是：
> 用 JavaScript 在后台向服务器发请求  
> 不刷新整个页面  
> 只更新页面的一部分
###### 没有Ajax时发生什么？
传统Web是：
1. 点击按钮
2. 浏览器向服务器发请求
3. 服务器返回完整HTML页面
4. 浏览器整个页面刷新
###### 有Ajax时发生什么？
流程
1. 点击按钮
2. JavaScript发请求（后台）
3. 服务器返回一小段数据
4. 页面只更新某个区域
###### Ajax例子
```
fetch("/api/data")
  .then(response => response.json())
  .then(data => {
    document.getElementById("result").innerText = data.value;
  });
```
- 向服务器请求数据
- 不刷新页面
- 把结果写进某个div
###### JSF中的Ajax是什么？
JSF用的是：
`<f:ajax render="outputArea" />`
发生的事情是：
1. 只提交当前组件
2. JSF在后台走生命周期
3. 服务器返回一段XML（partial response）
4. 浏览器用JS替换指定区域
###### JSF Ajax内部机制
JSF Ajax依赖三样东西：
1. ViewState（页面状态）
2. component tree（组件树）
3. partial response机制
服务器返回的不是完整HTML，而是：
```
<partial-response>
  <changes>
    <update id="form:outputArea">
      <![CDATA[新HTML内容]]>
    </update>
  </changes>
</partial-response>
```
然后JS在浏览器中：
- 找到 id="form:outputArea"
- 用新内容替换
###### 为什么Ajax容易出问题？
因为它依赖：
- DOM结构准确
- ID完全一致
- Cookie正常
- Session正常
- JS执行顺序正常
只要有一个出错：
- 区域不刷新
- 刷新错地方
- 报ViewExpiredException
- 页面假死
###### Chrome和Edge为什么会影响Ajax？
因为Ajax依赖：
- Cookie（Session）
- SameSite策略
- JS执行顺序
- DOM ready时机
- 安全策略
如果Chrome：
- 丢cookie
- 阻止请求
- JS顺序不同
Ajax就会失败。
如果出现：
- 点击后局部不刷新
- 刷新区域错乱
- 登录画面异常
第一怀疑：
👉 Ajax + ViewState + Cookie
而不是后端SQL。
###### 为什么JSF迁移后Ajax更敏感？
JSF是组件驱动框架。
它的Ajax不是简单fetch，而是：
- 依赖组件树
- 依赖ViewState
- 依赖ID生成规则
DOM结构一变，JSF Ajax就容易出问题。
##### Ajax的DOM定位和ID的关系
Ajax **不一定**必须用 ID  
但在 **JSF 体系里，几乎必然依赖 ID**
###### Ajax本身是不是必须用ID？
Ajax本质只是：
> 浏览器后台发请求 + 拿到结果 + 更新页面
更新页面时，可以用：
- ID
- class
- querySelector
- CSS选择器
- XPath
- 甚至直接替换整个innerHTML
例如：
```
document.querySelector(".result").innerHTML = data;
```
不需要一定ID，只是操作DOM的一种方式
###### 那为什么JSF几乎一定依赖ID
JSF不是你自己写：`fetch(...)`
JSF的Ajax是框架自动生成的。
JSF在服务器端知道的是：
> 组件树（component tree）
而组件在HTML里对应的唯一标识就是：`id="form:input1"`
JSF返回的是：
```
<update id="form:outputArea">
   <![CDATA[新的HTML]]>
</update>
```
浏览器收到后会：
`document.getElementById("form:outputArea")`

> JSF Ajax 的定位机制是基于组件ID的。
不是因为Ajax必须用ID，  
而是因为：
👉 JSF的设计是组件驱动，而组件靠ID定位。

##### 关于组件树 以及 JSF 
###### 什么是“组件树（Component Tree）
在 JSF 中：
> 页面不是“HTML文件”  
> 而是“组件的树结构”
```
<h:form>
    <h:inputText value="#{bean.name}" />
    <h:commandButton value="保存" />
</h:form>
```
在 JSF 看来，不是 HTML，而是：
```
UIViewRoot
 └── UIForm
      ├── UIInput
      └── UICommand
```
存在于 服务器端内存中。不是浏览器里的 DOM。
###### 组件树 vs HTML DOM
![[Pasted image 20260302134858.png]]
###### JSF Ajax 是怎么用组件树工作的
<f:ajax render="outputArea"/>
流程是：
1️⃣ 浏览器发 Ajax 请求  
2️⃣ 服务器恢复组件树（Restore View）  
3️⃣ JSF在组件树里找到 outputArea  
4️⃣ 重新渲染该组件  
5️⃣ 只把这一段 HTML 返回给浏览器
返回内容：
```
<partial-response>
  <update id="form:outputArea">
    <![CDATA[
        <span>新的内容</span>
    ]]>
  </update>
</partial-response>
```
Browser作业:
`document.getElementById("form:outputArea")`
替换之前的内容
###### 为什么组件树会成为风险点
JSF的页面状态完全依赖组件树。
组件树依赖：
- 唯一ID
- ViewState
- 组件层级结构
如果有差异：
**情况1：ID生成规则变化**
Teeda时代生成：
`input1`
JSF生成：
`form:input1`
JS代码写死旧ID → Ajax更新失效。

**情况2：浏览器丢Cookie**
Chrome因为SameSite丢Session
服务器无法恢复原组件树
→ ViewExpiredException

**情况3：DOM加载顺序差异**
JS在Chrome先执行
但组件还没完全ready
→ 找不到ID
##### 怎么确定项目中使用了 Ajax没有 
背景：Eclipse中用Ctrl+H检索了”ajax”关键词，但是没有搜索到对应的Xhtml时
###### 方法1：看浏览器 Network
操作页面，比如：
- 点击查询按钮
- 下拉框变化
- 输入框失焦
如果你看到：
- 请求发出
- 但页面没有整体刷新
- 返回类型是：
text/xml
application/xml
或 Response 里包含： 
```
<partial-response>
```
那就是 JSF Ajax。
###### 方法2：看页面有没有全刷新
- 页面白一下 → 全刷新
- 页面不闪，只局部更新 → Ajax
###### 方法3 搜索相关
- 搜 `<f:ajax` 这是 JSF 原生 Ajax。
- 搜 `<p:ajax`（如果用了PrimeFaces）如果项目用了 PrimeFaces
- 搜 `jsf.ajax`
- 搜 `onevent=` JSF Ajax 事件回调常见
###### 如果完全没有 `<f:ajax` 呢？
**① h:commandButton + 默认 Ajax**
某些组件库默认开启 Ajax。
例如 PrimeFaces 的：
```
<p:commandButton />
```
默认就是ajax


### Chromium差异机制
#### ① 默认安全策略差异

Chrome默认：
- SameSite=Lax
- Mixed Content拦截更严格
- 部分API默认开启
Edge某些版本可能策略宽松。

#### ② Cookie处理机制
如果：
- SameSite=None但未Secure
- domain/path不一致
Chrome会丢弃cookie。

这会导致：
- Session失效
- ViewState异常
- 登录反复跳转
#### ③ JS引擎优化差异

V8虽然同源，但版本不同。
不同优化策略可能导致：
- 执行顺序微差
- GC时机不同
- setTimeout精度差异

这些都可能影响：
- 批量DOM操作页面
- 高频事件页面