---
title: "C++ 连接数据库教程"
date: 2025-04-27T18:34:25+08:00
lastmod: 2025-04-27T21:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- 数据库
- C++
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: ""
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
---

# C++连接数据库教程

## 前言

现在使用C++写通信工具，需要使用C++连接数据库，就搜集了一下相关内容。

参考资料：

[实例讲解C++连接各种数据库，包含SQL Server、MySQL、Oracle、ACCESS、SQLite 和 PostgreSQL、MongoDB 数据库](https://www.cnblogs.com/hanbing81868164/p/17848051.html "发布于 2023-11-22 08:29")

## 连接到常用数据库

C++ 是一种通用的编程语言，可以使用不同的库和驱动程序来连接各种数据库。以下是一些示例代码，演示如何使用 C++ 连接 SQL Server、MySQL、Oracle、ACCESS、SQLite、PostgreSQL和MongoDB 数据库。

注意：下面的内容仅供参考，我没有完整测试其中内容的正确性。

### 连接 MySQL 数据库

要使用 C++ 连接 MySQL 数据库，可以使用 MySQL Connector/C++ 库。以下是一个示例代码：

```cpp
#include <mysql_driver.h>
#include <mysql_connection.h>
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/statement.h>

int main() {
    sql::mysql::MySQL_Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::ResultSet *res;

    driver = sql::mysql::get_mysql_driver_instance(); // 获取 MySQL 驱动程序实例
    con = driver->connect("tcp://localhost:3306", "user", "password"); // 连接数据库
    stmt = con->createStatement(); // 创建 Statement 对象
    res = stmt->executeQuery("SELECT * FROM MyTable"); // 执行查询并返回结果集

    while (res->next()) { // 遍历结果集
        // 处理数据
    }

    delete res; // 删除结果集对象
    delete stmt; // 删除 Statement 对象
    delete con; // 删除连接对象
    return 0;
}
```

### 连接 SQLite 数据库

要使用 C++ 连接 SQLite 数据库，可以使用SQLite C++库。以下是一个示例代码：

```cpp
#include <iostream>
#include <sqlite3.h>
#include <cassert>

int main() {
    sqlite3* db;
    int rc;
    std::string sql;

    // 打开数据库
    rc = sqlite3_open("MyDatabase.db", &db);
    assert(rc == SQLITE_OK);

    // 创建表格
    sql = "CREATE TABLE IF NOT EXISTS MyTable(id INTEGER PRIMARY KEY, name TEXT);";
    rc = sqlite3_exec(db, sql.c_str(), NULL, NULL, NULL);
    assert(rc == SQLITE_OK);

    // 插入数据
    sql = "INSERT INTO MyTable(name) VALUES('hello');";
    rc = sqlite3_exec(db, sql.c_str(), NULL, NULL, NULL);
    assert(rc == SQLITE_OK);

    // 查询数据
    sql = "SELECT * FROM MyTable;";
    rc = sqlite3_exec(db, sql.c_str(), callback, 0, 0);
    assert(rc == SQLITE_OK);

    // 关闭数据库
    sqlite3_close(db);
    return 0;
}
```

注意：如果编译器显示`#include <sqlite3.h>`这里有错，就改成`#include "sqlite3.h"`。

使用前需要把`sqlite3.h`和`sqlite3.c`文件放到项目根目录，和`main.cpp`在同一级别。

### 连接 PostgreSQL 数据库

要使用 C++ 连接 PostgreSQL 数据库，可以使用 PostgreSQL C++ 驱动程序。以下是一个示例代码：

```cpp
#include <iostream>
#include <postgresql/libpq-fe.h>
#include <cassert>

void callback(void* arg, int argc, char** argv, char** cols) {
    for (int i = 0; i < argc; i++) {
        std::cout << cols[i] << ": " << argv[i] << std::endl;
    }
}

int main() {
    PGconn* conn = PQconnectdb("host=localhost dbname=MyDatabase user=user password=password");
    assert(PQstatus(conn) == CONNECTION_OK);

    // 执行查询
    PGresult* res = PQexec(conn, "SELECT * FROM MyTable");
    assert(PQresultStatus(res) == PGRES_TUPLES_OK);

    // 遍历结果集
    for (int i = 0; i < PQntuples(res); i++) {
        callback(NULL, PQnfields(res), PQgetvalue(res, i), PQgetisnull(res, i));
    }

    // 关闭连接
    PQfinish(conn);
    return 0;
}
```

### 连接 MongoDB 数据库

```cpp
#include <iostream>
#include <mongocxx/client.hpp>
#include <mongocxx/instance.hpp>
#include <bsoncxx/json.hpp>
#include <bsoncxx/types.hpp>

int main() {
    mongocxx::instance instance{};
    mongocxx::client conn{mongocxx::uri{"mongodb://localhost:27017"}};

    // 连接到数据库
    mongocxx::database db = conn["MyDatabase"];

    // 创建文档
    bsoncxx::builder::stream::document doc{};
    doc << "name" << "John Doe"
        << "age" << 30
        << "email" << "johndoe@example.com";

    // 插入文档到集合
    db["MyCollection"].insert(doc.view());

    // 查询文档
    mongocxx::cursor cursor = db["MyCollection"].find({});
    while (cursor) {
        bsoncxx::document::view doc = cursor->view();
        std::cout << doc["name"].get_string() << std::endl;
        std::cout << doc["age"].get_int32() << std::endl;
        std::cout << doc["email"].get_string() << std::endl;
        cursor++;
    }

    return 0;
}
```

这个示例使用了MongoDB C++驱动程序来连接到MongoDB数据库，创建文档并将其插入到集合中，然后查询并打印文档的内容。

### 连接 SQL Server 数据库

要使用 C++ 连接 SQL Server 数据库，可以使用 Microsoft 的 ADODB 库。以下是一个示例代码：

```cpp
#include <iostream>
#import "C:\Program Files\Common Files\System\ado\msado15.dll" no_namespace rename("EOF", "EndOfFile")

int main() {
    CoInitialize(NULL); // 初始化 COM 库
    _ConnectionPtr pConnection("ADODB.Connection"); // 创建 Connection 对象
    _bstr_t strConnect = "Provider=SQLOLEDB;Data Source=localhost;Initial Catalog=MyDatabase;User ID=sa;Password=123456"; // 连接字符串
    pConnection->Open(strConnect, NULL, NULL, NULL); // 连接数据库

    if (pConnection->State) {
        _CommandPtr pCommand("ADODB.Command"); // 创建 Command 对象
        _bstr_t strSQL = "SELECT * FROM MyTable"; // SQL 查询语句
        pCommand->ActiveConnection = pConnection; // 设置连接对象
        pCommand->CommandText = strSQL; // 设置 SQL 语句
        _RecordsetPtr pRecordset("ADODB.Recordset"); // 创建 Recordset 对象
        pRecordset->Open(pCommand.GetInterfacePtr(), _variant_t((IDispatch *) pConnection, true), adOpenUnspecified, adLockUnspecified, -1); // 执行查询并返回结果集

        while (!pRecordset->EndOfFile) { // 遍历结果集
            // 处理数据
        }
    }

    pConnection->Close(); // 关闭连接
    CoUninitialize(); // 关闭 COM 库
    return 0;
}
```

### 连接 Oracle 数据库

要使用 C++ 连接 Oracle 数据库，可以使用 Oracle 提供的 ODBC 驱动程序。以下是一个示例代码：

```cpp
#include <iostream>
#include <windows.h>
#include <occi.h>

using namespace oracle::occi;

int main() {
    Environment *env = Environment::createEnvironment(); // 创建 OCCI 环境
    Connection *conn = env->createConnection("DRIVER={Oracle ODBC Driver};SERVER=localhost;DATABASE=MyDatabase;UID=user;PWD=password"); // 连接数据库

    if (conn->isValid()) {
        Statement *stmt = conn->createStatement("SELECT * FROM MyTable"); // 创建 Statement 对象
        ResultSet *res = stmt->executeQuery(); // 执行查询并返回结果集

        while (res->next()) { // 遍历结果集
            // 处理数据
        }
    }

    conn->close(); // 关闭连接
    env->terminate(); // 关闭 OCCI 环境
    return 0;
}
```

### 连接 Access 数据库

要使用 C++ 连接 Access 数据库，可以使用 Microsoft 的 ADODB 库。以下是一个示例代码：

```cpp
#include <iostream>
#import "C:\Program Files\Common Files\System\ado\msado15.dll" no_namespace rename("EOF", "EndOfFile")

int main() {
    CoInitialize(NULL); // 初始化 COM 库
    _ConnectionPtr pConnection("ADODB.Connection"); // 创建 Connection 对象
    _bstr_t strConnect = "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\\MyDatabase.mdb;Persist Security Info=False"; // 连接字符串
    pConnection->Open(strConnect, "", "", adConnectUnspecified); // 连接数据库

    if (pConnection->State) {
        _CommandPtr pCommand("ADODB.Command"); // 创建 Command 对象
        _bstr_t strSQL = "SELECT * FROM MyTable"; // SQL 查询语句
        pCommand->ActiveConnection = pConnection; // 设置连接对象
        pCommand->CommandText = strSQL; // 设置 SQL 语句
        _RecordsetPtr pRecordset("ADODB.Recordset"); // 创建 Recordset 对象
        pRecordset->Open(pCommand.GetInterfacePtr(), _variant_t((IDispatch *) pConnection, true), adOpenUnspecified, adLockUnspecified, -1); // 执行查询并返回结果集

        while (!pRecordset->EndOfFile) { // 遍历结果集
            // 处理数据
        }
    }

    pConnection->Close(); // 关闭连接
    CoUninitialize(); // 关闭 COM 库
    return 0;
}
```

