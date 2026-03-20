# Firebase 配置指南

## 📋 项目已完成功能

✅ 用户注册系统（register.html）
✅ 用户登录系统（login.html）
✅ 管理后台（admin.html）- 可修改产品和招聘信息
✅ 主页和招聘页面已集成登录状态检测
✅ Firebase 数据库集成

---

## 🔧 Firebase 配置步骤

### 第一步：创建 Firebase 项目

1. 打开 [Firebase Console](https://console.firebase.google.com/)
2. 点击 **"创建项目"**（或 **"Add project"**）
3. 项目名称：输入 `mufet-website`（或其他你喜欢的名字）
4. 选择 Google Analytics：可以暂时关闭（节省时间）
5. 点击 **"创建项目"**，等待 1-2 分钟

---

### 第二步：启用身份验证（Authentication）

1. 在左侧菜单找到 **"Authentication"**（或 **"身份验证"**）
2. 点击 **"开始使用"**（**"Get started"**）
3. 选择 **"电子邮箱/密码"**（**"Email/Password"**）
4. 启用它，点击 **"保存"**
5. 在 **"登录提供程序"**（**"Sign-in method"**）标签页，确保 **"电子邮箱/密码"** 已启用

---

### 第三步：启用实时数据库（Realtime Database）

1. 在左侧菜单找到 **"Realtime Database"**（**"实时数据库"**）
2. 点击 **"创建数据库"**（**"Create database"**）
3. 选择位置：选择 `us-central1`（美国中部）或 `asia-southeast1`（东南亚，对中国更友好）
4. 安全规则：选择 **"测试模式"**（**"Test mode"**）
   - ⚠️ 注意：测试模式允许任何人读写，仅用于开发！
   - 生产环境请使用 **"锁定模式"**（**"Locked mode"**）并配置适当规则
5. 点击 **"启用"**（**"Enable"**）

---

### 第四步：获取 Firebase 配置信息

1. 点击左侧菜单的 **"项目设置"**（**"Project Settings"**，齿轮图标）
2. 向下滚动，找到 **"您的应用"**（**"Your apps"**）部分
3. 点击 **</>** 图标（**"Web"**）
4. 应用昵称：输入 `mufet-web`
5. 点击 **"注册应用"**（**"Register app"**）
6. **不需要**勾选 Firebase Hosting
7. 点击 **"继续到控制台"**（**"Continue to console"**）
8. 复制显示的 **"Firebase SDK 配置"** 代码，格式如下：

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyxxxxxxxxxxxxxx",
  authDomain: "mufet-website.firebaseapp.com",
  projectId: "mufet-website",
  storageBucket: "mufet-website.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef123456"
};
```

---

### 第五步：替换所有 HTML 文件中的配置

你需要修改以下 4 个文件中的 `firebaseConfig`：

1. ✅ `mufet_products.html`
2. ✅ `recruitment.html`
3. ✅ `login.html`
4. ✅ `register.html`
5. ✅ `admin.html`

**在每个文件中找到这段代码：**

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

**替换为你从 Firebase 复制的实际配置：**

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyxxxxxxxxxxxxxx",  // 替换为你的 API Key
    authDomain: "mufet-website.firebaseapp.com",  // 替换为你的项目 ID
    projectId: "mufet-website",  // 替换为你的项目 ID
    storageBucket: "mufet-website.appspot.com",  // 替换为你的项目 ID
    messagingSenderId: "123456789",  // 替换为你的发送者 ID
    appId: "1:123456789:web:abcdef123456"  // 替换为你的应用 ID
};
```

---

### 第六步：推送代码到 GitHub

```powershell
cd C:\Users\user\Desktop\mosfet
git add .
git commit -m "Add Firebase authentication and admin panel"
git push
```

---

### 第七步：测试完整流程

1. **访问主页**：`https://chenst-uuui.github.io/mosfet-website/mufet_products.html`
2. **点击"登录"按钮**，跳转到登录页面
3. **注册新账号**：
   - 输入邮箱和密码
   - 点击注册
   - 成功后自动跳转到管理后台
4. **在管理后台修改信息**：
   - 修改产品信息或招聘信息
   - 点击保存
5. **退出登录**
6. **再次登录**
7. 查看修改后的信息是否保存成功

---

## ⚠️ 重要提示

### 开发模式 vs 生产模式

**当前配置使用的是测试模式（允许任何人读写数据库），仅用于开发！**

如果要上线，请在 Firebase Console → Realtime Database → **"规则"**（**"Rules"**）标签页，修改为：

```javascript
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

这样只有登录用户才能读写数据库。

---

### 数据库结构

Firebase 实时数据库中会存储两个节点：

```
mufet-website-default-rtdb/
├── products/
│   ├── prod1Name: "产品1名称"
│   ├── prod1Desc: "产品1描述"
│   ├── prod2Name: "产品2名称"
│   └── prod2Desc: "产品2描述"
└── recruitment/
    ├── contactPerson: "曾少通"
    ├── contactPhone: "18186023396"
    └── companyAddress: "上海市奉贤区莘奉公路4869号1层"
```

---

## 🆘 常见问题

### Q1: 点击注册/登录没反应？
**A**: 检查浏览器控制台（F12）是否有错误，确认 Firebase 配置是否正确。

### Q2: 注册成功但无法登录？
**A**: 检查邮箱是否需要验证（Authentication → Users）。

### Q3: 保存信息失败？
**A**: 检查 Realtime Database 规则是否允许写入。

### Q4: 数据库显示 403 错误？
**A**: 检查 Firebase 项目 ID 是否正确，以及 API Key 是否有效。

---

## 📞 技术支持

如有问题，请检查：
1. Firebase Console 中是否有错误提示
2. 浏览器控制台（F12）的错误信息
3. 确认所有 5 个 HTML 文件的 Firebase 配置都已更新

---

**配置完成后，你的网站就拥有了完整的用户系统和数据管理功能！** 🎉
