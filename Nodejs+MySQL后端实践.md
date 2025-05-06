# Nodejs+MySQL后端实践

以下是利用npm创建Node.js+MySQL后端应用的详细步骤，结合多个最佳实践和最新技术方案：

## 一、项目初始化与依赖安装

1. 创建项目目录并初始化

   ```bash
   mkdir my-node-mysql-app && cd my-node-mysql-app
   npm init -y  # 快速生成package.json
   ```

2. 安装核心依赖

    mysql2就是对sql 命令的封装的对象

   ```bash
   npm install express mysql2 cors  # 包含Express框架、MySQL驱动和跨域支持
   ```

3. 开发依赖（可选）

   

   ```bash
   npm install nodemon --save-dev  # 支持热重载开发
   ```

## 二、数据库配置

1. 创建数据库连接文件（db.js）

   ```javascript
   // 使用连接池提升性能
   const mysql = require('mysql2/promise');
   
   //构造链接池
   const pool = mysql.createPool({
     host: 'localhost',
     user: 'root',//连接用户名
     password: 'wh050219', //链接用户密码
     database: 'test',  //链接数据库名
     waitForConnections: true, //允许排队
     connectionLimit: 10  // 连接池大小
   });
   
   module.exports = pool;
   ```

2. 创建数据库表

   在Navicat的查询中创建test数据库，增加用户表

   ```sql
   CREATE TABLE IF NOT EXISTS users (
     id INT AUTO_INCREMENT PRIMARY KEY,
     name VARCHAR(50) NOT NULL,
     email VARCHAR(100) UNIQUE NOT NULL,
     created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

## 三、Express服务器搭建

1. 基础服务配置（app.js）

   ```javascript
   const express = require('express');
   const cors = require('cors');
   const pool = require('./db');
   
   const app = express();
   const PORT = 3000; //后端运行的端口
   
   // 中间件配置
   app.use(cors()); //跨域请求中间件，解决跨域请求问题
   app.use(express.json());  // 解析JSON请求体
   ```

2. CRUD路由示例

   ```javascript
   // 获取所有用户
   app.get('/users', async (req, res) => {
     try {
       const [rows] = await pool.query('SELECT * FROM users');
       res.json(rows);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: 'Database query failed' });
     }
   });
   
   // 创建用户
   app.post('/users', async (req, res) => {
     const { name, email } = req.body;
     try {
       const [result] = await pool.execute(
         'INSERT INTO users (name, email) VALUES (?, ?)',
         [name, email]
       );
       res.status(201).json({ id: result.insertId });
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: 'User creation failed' });
     }
   });
   
     //监听端口，这里定义的是3000，访问的也是3000
   app.listen(PORT, () => {
       console.log(`Server is running on http://localhost:${PORT}`);
     });
   
     // 统一错误处理中间件
   app.use((err, req, res, next) => {
       console.error(err.stack);
       res.status(500).json({ error: 'Internal Server Error' });
     });
   ```

## 四、启动与测试

1. 配置启动脚本（package.json文件）

   

   ```json
   "scripts": {
     "start": "node app.js",
     "dev": "nodemon app.js"
   }
   ```

2. 运行服务

   ```bash
   npm run dev  # 开发模式启动
   ```

3. 测试API

   在powershell中利用Invoke-WebRequest进行请求测试

   ```bash
   Invoke-WebRequest -Uri "http://localhost:3000/users" `
   -Method POST `
   -ContentType "application/json" `
   -Body '{"name":"John","email":"john@example.com"}'
   ```

## 五、最佳实践

1. 安全配置
    • 使用环境变量管理数据库凭证（dotenv包）

   • 参数化查询防止SQL注入

   • 启用HTTPS加密传输

2. 性能优化
    • 连接池复用数据库连接

   • 添加请求速率限制

   • 实现缓存机制（Redis）

3. 错误处理

   ```javascript
   // 统一错误处理中间件
   app.use((err, req, res, next) => {
     console.error(err.stack);
     res.status(500).json({ error: 'Internal Server Error' });
   });
   ```

扩展建议
 • 使用ORM工具（如Sequelize）简化数据库操作

• 实现JWT认证中间件

• 添加API文档（Swagger）

• 配置数据库迁移工具（Knex.js）

