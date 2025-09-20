# 服务

```js
import express from "express";
import bodyParser from "body-parser";

const app = express();

// 解析application/json类型的body
app.use(bodyParser.json());
// 解析 application/x-www-form-urlencoded类型的body
app.use(bodyParser.urlencoded({ extended: true }));

app.use(
  (req: express.Request, res: express.Response, next: express.NextFunction) => {
    const method = req.method;
    const urlObj = url.parse(req.url, true);
    const params = method === "GET" ? urlObj.query : req.body;

    log(
      `\n${formatDate()}：【${method}】【${urlObj.pathname}】 ${JSON.stringify(
        params
      )}`
    );

    next();
  }
);

// 端口
const port = 3000;

app.listen(port, () => {
  console.log("\x1b[34m%s\x1b[0m", `地址: http://localhost:${port}`);
});
```

# 链接 Oracle 数据库

- 安装 `Oracle Instant Client` ，需要与安装的 `Oracle` 版本一致

  1.  `window` [下载地址](https://www.oracle.com/cn/database/technologies/instant-client/winx64-64-downloads.html)
  1.  `Mac` [下载地址](https://www.oracle.com/database/technologies/instant-client/macos-intel-x86-downloads.html)
  1.  下载 `Package - Basic` 版本即可

- `windows` 环境下需设置环境变量
  1.  右键点击 `此电脑` 或 `计算机`，选择属性；
  1.  点击 `系统高级设置`，然后点击 `环境变量`；
  1.  找到 `Path` 变量，添加你的 `Oracle Instant Client` 解压路径；
- `Mac` 环境需要将文件解压到到指定目录
  1.  方达 -> 右键 -> 前往文件夹 `/usr/local/lib`；
  1.  将下载的压缩文件双击解出来的文件拷贝到 `/usr/local/lib` 目录下；
  1.  注意的拷贝的是压缩文件内的文件，非文件夹！！！

```js
import oracledb from "oracledb";

const DB_CONFIG = {
  user: "orcale",
  password: "123456",
  // 数据库地址： IP:端口号/数据库名称-sid
  connectString: "127.0.0.1:1521/orcl",
  // 在创建连接池时，你需要明确指定它将用于异构。这通常通过在池创建过程中设置特定选项来完成，例如 homogeneous: false 或根据 node-oracledb 版本和你的配置类似的配置。使用代理凭据获取连接。
  homogeneous: false,
};

export const createClient = async () => {
  let pool, connection;
  try {
    pool = await oracledb.createPool(DB_CONFIG);
    connection = await pool.getConnection(DB_CONFIG);

    connection = await pool.getConnection();
    // 执行 SQL 查询
    let results = await connection.execute(
      // `SELECT 'Hello from Oracle!' AS message FROM DUAL`,
      // `SELECT * FROM all_tables WHERE table_name = 'TEST_USER'`,
      `SELECT * FROM TEST_USER`,
      [],
      { outFormat: oracledb.OUT_FORMAT_OBJECT }
    );
    console.log(results.rows);
  } catch (err) {
    console.log(err);
  } finally {
    console.log(connection);
    if (connection) {
      try {
        await connection.close();
        await pool.close();
      } catch (err) {
        console.error("关闭连接错误:", err);
      }
    }
  }
};
```

# 封装

```js

class Oracle {
  // 创建连接池
  async createPool() {
    let pool: oracledb.Pool
    try {
      pool = await oracledb.createPool(DB_CONFIG)
    } catch (e) {
      throw e
    }
    return pool
  }

  // 创建连接
  async createConnection(pool: oracledb.Pool) {
    let connection
    try {
      connection = await pool.getConnection()
    } catch (e) {
      throw e
    }
    return connection
  }

  // 查询
  query(
  	// 查询语句
    sql: string,
    // 字段映射
    mapping: { [key: string]: string } = {},
    binds: oracledb.BindParameters = [],
    options: oracledb.ExecuteOptions = { outFormat: oracledb.OUT_FORMAT_OBJECT }
  ) {
    let pool: oracledb.Pool
    let connection: oracledb.Connection
    return new Promise(async (resolve, reject) => {
      try {
        pool = await this.createPool()
        try {
          connection = await this.createConnection(pool)
          const result = await connection.execute(sql, binds, options)

          // 字段映射
          const keys = Object.keys(mapping)
          const values = Object.values(mapping)

          resolve(
            result?.rows?.map((item: any) =>
              result.metaData?.reduce((pre, curr, index) => {
                const key = curr.name
                const mapKey = keys[values.findIndex(k => k == key)]
                if (mapKey) {
                  let val = item[key]
                  if (val instanceof Date) {
                    val = formatDate(val)
                  }
                  pre[mapKey] = val
                }
                return pre
              }, {} as any)
            )
          )
        } catch (e) {
          throw e
        } finally {
          if (connection) {
            try {
              await connection.close()
            } catch (e) {
              throw e
            }
          }
        }
      } catch (e) {
        reject(e)
      } finally {
        if (pool) {
          try {
            await pool.close()
          } catch (e) {
            throw e
          }
        }
      }
    })
  }
}

const oracle = new Oracle()

export default {
  async query(
    sql: string,
    mapping: { [key: string]: string } = {},
    binds?: oracledb.BindParameters,
    options?: oracledb.ExecuteOptions
  ) {
    return await oracle.query(sql, mapping, binds, options)
  }
}
```

```js
// 查询表中第一条数据
DB.query(`SELECT * FROM (SELECT * FROM TEST_USER) WHERE ROWNUM = 1`, {
  id: "ID",
}).then((res) => {
  console.log(res);
});

// 查询表中最后一条数据
DB.query(
  `SELECT * from(SELECT * FROM TEST_USER ORDER BY ID DESC ) WHERE ROWNUM = 1`,
  { id: "ID" }
).then((res) => {
  console.log(res);
});
```

```js
// 查询时间范围
const startDate = new Date("2023-01-01"); // 开始日期
const endDate = new Date("2023-01-31"); // 结束日期（包含当天）
const sql = `SELECT * FROM my_table WHERE my_date_column BETWEEN :start_date AND :end_date`;

DB.query(sql, { id: "ID" }, { start_date: startDate, end_date: endDate }).then(
  (res) => {
    console.log(res);
  }
);
```

```js
// 插入数据
const values = [userName, email, datetime ? new Date(datetime) : new Date()];
const sql = `INSERT INTO TEST_USER (USER_NAME, EMAIL, CREATE_TIME, ID) VALUES (:1, :2, :3)`;
DB.insert(sql, values).then((res) => {
  console.log(res);
});
```

# 注意项

- 插入表数据时，`MODE` 字段使用时需要加上双引号，否则会报错
