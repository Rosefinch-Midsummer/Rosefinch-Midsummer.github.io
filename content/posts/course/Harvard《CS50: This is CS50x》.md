---
title: "Harvard《CS50: This is CS50x》"
date: 2025-12-06T19:34:25+08:00
lastmod: 2025-12-06T22:54:22+08:00
categories:
- 在线课程
- 计算机
tags:
- Harvard
- CS50
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


# 课程简介

- 所属大学：Harvard
- 先修要求：无
- 编程语言：C, Python, SQL, HTML, CSS, JavaScript
- 课程难度：🌟🌟
- 预计学时：20 小时

连续多年被哈佛大学学生评为最受欢迎的公选课程。Malan 教授上课非常有激情，撕黄页讲二分法的场面让人记忆犹新（笑）。但因为它的入门以及全校公选的属性，课程内容难度比较温和，但是课程作业质量非常高而且全部免费开源，非常适合小白入门，或者大佬休闲。

# 课程资源

- 课程网站：[2025](https://cs50.harvard.edu/x/2025/), [2024](https://cs50.harvard.edu/x/2024/), [2023](https://cs50.harvard.edu/x/2023/), [2022](https://cs50.harvard.edu/x/2022/)
- 课程视频：原版参考课程网站，也可以在 B 站找到[中文字幕版](https://www.bilibili.com/video/BV1HW4y1A7Yi/?spm_id_from=333.999.0.0&vd_source=a4d76d1247665a7e7bec15d15fd12349)。
- 课程教材：无
- 课程作业：参考课程网站。

# 资源汇总

@mancuoj 在学习这门课中用到的所有资源和作业实现都汇总在 [mancuoj/CS50x - GitHub](https://github.com/mancuoj/CS50x) 中。

@figuretu 将有价值的提问讨论以及相关学习资源整理在共享文档 [CS50 - 资源总目录](https://uufyjevghz.feishu.cn/docx/DP78d2U5TosTOTx9QCbcjp8GnBh) 中。


# Notes

## [C——Command-Line Arguments](https://cs50.harvard.edu/x/notes/2/#command-line-arguments)

- `Command-line arguments` are those arguments that are passed to your program at the command line. For example, all those statements you typed after `clang` are considered command line arguments. You can use these arguments in your own programs!
- In your terminal window, type `code greet.c` and write code as follows:
    
    ```
    // Uses get_string
    
    #include <cs50.h>
    #include <stdio.h>
    
    int main(void)
    {
        string answer = get_string("What's your name? ");
        printf("hello, %s\n", answer);
    }
    ```
    
    Notice that this says `hello` to the user.
    
- Still, would it not be nice to be able to take arguments before the program even runs? Modify your code as follows:
    
    ```
    // Prints a command-line argument
    
    #include <cs50.h>
    #include <stdio.h>
    
    int main(int argc, string argv[])
    {
        if (argc == 2)
        {
            printf("hello, %s\n", argv[1]);
        }
        else
        {
            printf("hello, world\n");
        }
    }
    ```
    
    Notice that this program knows both `argc`, the number of command line arguments, and `argv`, which is an array of the characters passed as arguments at the command line.
    
- Therefore, using the syntax of this program, executing `./greet David` would result in the program saying `hello, David`.
- You can print each of the command-line arguments with the following:
    
    ```
    // Prints command-line arguments
    
    #include <cs50.h>
    #include <stdio.h>
    
    int main(int argc, string argv[])
    {
        for (int i = 0; i < argc; i++)
        {
            printf("%s\n", argv[i]);
        }
    }
    ```
    

## [C——Exit Status](https://cs50.harvard.edu/x/notes/2/#exit-status)

- When a program ends, a special exit code is provided to the computer.
- When a program exits without error, a status code of `0` is provided to the computer. Often, when an error occurs that results in the program ending, a status of `1` is provided by the computer.
- You could write a program as follows that illustrates this by typing `code status.c` and writing code as follows:
    
    ```
    // Returns explicit value from main
    
    #include <cs50.h>
    #include <stdio.h>
    
    int main(int argc, string argv[])
    {
        if (argc != 2)
        {
            printf("Missing command-line argument\n");
            return 1;
        }
        printf("hello, %s\n", argv[1]);
        return 0;
    }
    ```
    
    Notice that if you fail to provide `./status David`, you will get an exit status of `1`. However, if you do provide `./status David`, you will get an exit status of `0`.
    
- You can type `echo $?` in the terminal to see the exit status of the last run command.
- You can imagine how you might use portions of the above program to check if a user provided the correct number of command-line arguments.



## [Copying and malloc](https://cs50.harvard.edu/x/notes/4/#copying-and-malloc)

- A common need in programming is to copy one string to another.
- In your terminal window, type `code copy.c` and write code as follows:
    
    ```
    // Capitalizes a string
    
    #include <cs50.h>
    #include <ctype.h>
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        // Get a string
        string s = get_string("s: ");
    
        // Copy string's address
        string t = s;
    
        // Capitalize first letter in string
        t[0] = toupper(t[0]);
    
        // Print string twice
        printf("s: %s\n", s);
        printf("t: %s\n", t);
    }
    ```
    
    Notice that `string t = s` copies the address of `s` to `t`. This does not accomplish what we are desiring. The string is not copied – only the address is. Further, notice the inclusion of `ctype.h`.
    
- You can visualize the above code as follows:
    
    ![two pointers pointing at the same memory location with a string](https://cs50.harvard.edu/x/notes/4/cs50Week4Slide124.png "two strings")
    
    Notice that `s` and `t` are still pointing at the same blocks of memory. This is not an authentic copy of a string. Instead, these are two pointers pointing at the same string.
    
- Before we address this challenge, it’s important to ensure that we don’t experience a _segmentation fault_ through our code, where we attempt to copy `string s` to `string t`, where `string t` does not exist. We can employ the `strlen` function as follows to assist with that:
    
    ```
    // Capitalizes a string, checking length first
    
    #include <cs50.h>
    #include <ctype.h>
    #include <stdio.h>
    #include <string.h>
    
    int main(void)
    {
        // Get a string
        string s = get_string("s: ");
    
        // Copy string's address
        string t = s;
    
        // Capitalize first letter in string
        if (strlen(t) > 0)
        {
            t[0] = toupper(t[0]);
        }
    
        // Print string twice
        printf("s: %s\n", s);
        printf("t: %s\n", t);
    }
    ```
    
    Notice that `strlen` is used to make sure `string t` exists. If it does not, nothing will be copied.
    
- To be able to make an authentic copy of the string, we will need to introduce two new building blocks. First, `malloc` allows you, the programmer, to allocate a block of a specific size of memory. Second, `free` allows you to tell the compiler to _free up_ that block of memory you previously allocated.
    
- We can modify our code to create an authentic copy of our string as follows:
    
    ```
    // Capitalizes a copy of a string
    
    #include <cs50.h>
    #include <ctype.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    int main(void)
    {
        // Get a string
        char *s = get_string("s: ");
    
        // Allocate memory for another string
        char *t = malloc(strlen(s) + 1);
    
        // Copy string into memory, including '\0'
        for (int i = 0; i <= strlen(s); i++)
        {
            t[i] = s[i];
        }
    
        // Capitalize copy
        t[0] = toupper(t[0]);
    
        // Print strings
        printf("s: %s\n", s);
        printf("t: %s\n", t);
    }
    ```
    
    Notice that `malloc(strlen(s) + 1)` creates a block of memory that is the length of the string `s` plus one. This allows for the inclusion of the _null_ `\0` character in our final copied string. Then, the `for` loop walks through the string `s` and assigns each value to that same location on the string `t`.
    
- It turns out that our code is inefficient. Modify your code as follows:
    
    ```
    // Capitalizes a copy of a string, defining n in loop too
    
    #include <cs50.h>
    #include <ctype.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    int main(void)
    {
        // Get a string
        char *s = get_string("s: ");
    
        // Allocate memory for another string
        char *t = malloc(strlen(s) + 1);
    
        // Copy string into memory, including '\0'
        for (int i = 0, n = strlen(s); i <= n; i++)
        {
            t[i] = s[i];
        }
    
        // Capitalize copy
        t[0] = toupper(t[0]);
    
        // Print strings
        printf("s: %s\n", s);
        printf("t: %s\n", t);
    }
    ```
    
    Notice that `n = strlen(s)` is defined now in the left-hand side of the `for loop`. It’s best not to call unneeded functions in the middle condition of the `for` loop, as it will run over and over again. When moving `n = strlen(s)` to the left-hand side, the function `strlen` only runs once.
    
- The `C` Language has a built-in function to copy strings called `strcpy`. It can be implemented as follows:
    
    ```
    // Capitalizes a copy of a string using strcpy
    
    #include <cs50.h>
    #include <ctype.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    int main(void)
    {
        // Get a string
        char *s = get_string("s: ");
    
        // Allocate memory for another string
        char *t = malloc(strlen(s) + 1);
    
        // Copy string into memory
        strcpy(t, s);
    
        // Capitalize copy
        t[0] = toupper(t[0]);
    
        // Print strings
        printf("s: %s\n", s);
        printf("t: %s\n", t);
    }
    ```
    
    Notice that `strcpy` does the same work that our `for` loop previously did.
    
- Both `get_string` and `malloc` return `NULL`, a special value in memory, in the event that something goes wrong. You can write code that can check for this `NULL` condition as follows:
    
    ```
    // Capitalizes a copy of a string without memory errors
    
    #include <cs50.h>
    #include <ctype.h>
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    int main(void)
    {
        // Get a string
        char *s = get_string("s: ");
        if (s == NULL)
        {
            return 1;
        }
    
        // Allocate memory for another string
        char *t = malloc(strlen(s) + 1);
        if (t == NULL)
        {
            return 1;
        }
    
        // Copy string into memory
        strcpy(t, s);
    
        // Capitalize copy
        if (strlen(t) > 0)
        {
            t[0] = toupper(t[0]);
        }
    
        // Print strings
        printf("s: %s\n", s);
        printf("t: %s\n", t);
    
        // Free memory
        free(t);
        return 0;
    }
    ```
    
    Notice that if the string obtained is of length `0` or malloc fails, `NULL` is returned. Further, notice that `free` lets the computer know you are done with this block of memory you created via `malloc`.
    

## [Valgrind](https://cs50.harvard.edu/x/notes/4/#valgrind)

- _Valgrind_ is a tool that can check to see if there are memory-related issues with your programs wherein you utilized `malloc`. Specifically, it checks to see if you `free` all the memory you allocated.
- Consider the following code for `memory.c`:
    
    ```
    // Demonstrates memory errors via valgrind
    
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int *x = malloc(3 * sizeof(int));
        x[1] = 72;
        x[2] = 73;
        x[3] = 33;
    }
    ```
    
    Notice that running this program does not cause any errors. While `malloc` is used to allocate enough memory for an array, the code fails to `free` that allocated memory.
    
- If you type `make memory` followed by `valgrind ./memory`, you will get a report from valgrind that will report where memory has been lost as a result of your program. One error that valgrind reveals is that we attempted to assign the value of `33` at the 4th position of the array, where we only allocated an array of size `3`. Another error is that we never freed `x`.
- You can modify your code to free the memory of `x` as follows:
    
    ```
    // Demonstrates memory errors via valgrind
    
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int *x = malloc(3 * sizeof(int));
        x[1] = 72;
        x[2] = 73;
        x[3] = 33;
        free(x);
    }
    ```
    
    Notice that running valgrind again now results in no memory leaks.
    

## [Garbage Values](https://cs50.harvard.edu/x/notes/4/#garbage-values)

- When you ask the compiler for a block of memory, there is no guarantee that this memory will be empty.
- It’s very possible that the memory you allocated was previously utilized by the computer. Accordingly, you may see _junk_ or _garbage values_. This is a result of you getting a block of memory but not initializing it. For example, consider the following code for `garbage.c`:
    
    ```
    #include <stdio.h>
    #include <stdlib.h>
    
    int main(void)
    {
        int scores[1024];
        for (int i = 0; i < 1024; i++)
        {
            printf("%i\n", scores[i]);
        }
    }
    ```
    
    Notice that running this code will allocate `1024` locations in memory for your array, but the `for` loop will likely show that not all values therein are `0`. It’s always best practice to be aware of the potential for garbage values when you do not initialize blocks of memory to some other value like zero or otherwise.




## [Tries](https://cs50.harvard.edu/x/notes/5/#tries)

- _Tries_ are another form of data structure. Tries are trees of arrays.
- _Tries_ are always searchable in constant time.
- One downside to _Tries_ is that they tend to take up a large amount of memory. Notice that we need 26 ×4 =104 `node`s just to store _Toad_!
- _Toad_ would be stored as follows:
    
    ![toad being spelled with one letter at a time where one letter is associated with one list T from one list O from another and so on](https://cs50.harvard.edu/x/notes/5/cs50Week5Slide207.png "tries")
    
- _Tom_ would then be stored as follows:
    
    ![toad being spelled with one letter at a time where one letter is associated with one list T from one list O from another and so on and tom being spelled similarly where toad and tom share a two common letters T and O](https://cs50.harvard.edu/x/notes/5/cs50Week5Slide209.png "tries")
    
- This structure offers a search time of 𝑂⁡(1).
- The downside of this structure is how many resources are required to use it.


## [Python——Command-Line Arguments](https://cs50.harvard.edu/x/notes/6/#command-line-arguments)

- As with C, you can also utilize command-line arguments. Consider the following code:
    
    ```
    # Prints a command-line argument
    
    from sys import argv
    
    if len(argv) == 2:
        print(f"hello, {argv[1]}")
    else:
        print("hello, world")
    ```
    
    Notice that `argv[1]` is printed using a _formatted string_, noted by the `f` present in the `print` statement.
    
- You can learn more about the `sys` library in the [Python documentation](https://docs.python.org/3/library/sys.html)
    

## [Python——Exit Status](https://cs50.harvard.edu/x/notes/6/#exit-status)

- The `sys` library also has built-in methods. We can use `sys.exit(i)` to exit the program with a specific exit code:
    
    ```
    # Exits with explicit value, importing sys
    
    import sys
    
    if len(sys.argv) != 2:
        print("Missing command-line argument")
        sys.exit(1)
    
    print(f"hello, {sys.argv[1]}")
    sys.exit(0)
    ```
    
    Notice that dot-notation is used to utilize the built-in functions of `sys`.


## [Relational Databases](https://cs50.harvard.edu/x/notes/7/#relational-databases)

- Google, X, and Meta all use relational databases to store their information at scale.
- Relational databases store data in rows and columns in structures called _tables_.
- SQL allows for four types of commands:
    
    ```
      Create
      Read
      Update
      Delete
    ```
    
- These four operations are affectionately called _CRUD_.
- We can create a database with the SQL syntax `CREATE TABLE table (column type, ...);`. But where do you run this command?
- `sqlite3` is a type of SQL database that has the core features required for this course.
- We can create a SQL database at the terminal by typing `sqlite3 favorites.db`. Upon being prompted, we will agree that we want to create `favorites.db` by pressing `y`.
- You will notice a different prompt as we are now using a program called `sqlite`.
- We can put `sqlite` into `csv` mode by typing `.mode csv`. Then, we can import our data from our `csv` file by typing `.import favorites.csv favorites`. It seems that nothing has happened!
- We can type `.schema` to see the structure of the database.
- You can read items from a table using the syntax `SELECT columns FROM table`.
- For example, you can type `SELECT * FROM favorites;` which will print every row in `favorites`.
- You can get a subset of the data using the command `SELECT language FROM favorites;`.
- SQL supports many commands to access data, including:
    
    ```SQL
      AVG
      COUNT
      DISTINCT
      LOWER
      MAX
      MIN
      UPPER
    ```
    
- For example, you can type `SELECT COUNT(*) FROM favorites;`. Further, you can type `SELECT DISTINCT language FROM favorites;` to get a list of the individual languages within the database. You could even type `SELECT COUNT(DISTINCT language) FROM favorites;` to get a count of those.
- SQL offers additional commands we can utilize in our queries:
    
    ```
      WHERE       -- adding a Boolean expression to filter our data
      LIKE        -- filtering responses more loosely
      ORDER BY    -- ordering responses
      LIMIT       -- limiting the number of responses
      GROUP BY    -- grouping responses together
    ```
    
    Notice that we use `--` to write a comment in SQL.


## [SQL Injection Attacks](https://cs50.harvard.edu/x/notes/7/#sql-injection-attacks)

- Now, still considering the code above, you might be wondering what the `?` question marks do above. One of the problems that can arise in real-world applications of SQL is what is called an _injection attack_. An injection attack is where a malicious actor could input malicious SQL code.
- For example, consider a login screen as follows:
    
    ![harvard key login screen with username and password fields](https://cs50.harvard.edu/x/notes/7/cs50Week7Slide051.png "harvard key login screen")
    
- Without the proper protections in our own code, a bad actor could run malicious code. Consider the following:
    
    ```
    rows = db.execute("SELECT COUNT(*) FROM users WHERE username = ? AND password = ?", username, password)
    ```
    
    Notice that because the `?` is in place, validation can be run on `favorite` before it is blindly accepted by the query.
    
- You never want to utilize formatted strings in queries as above or blindly trust the user’s input.
- Utilizing the CS50 Library, the library will _sanitize_ and remove any potentially malicious characters.


## [http-server](https://cs50.harvard.edu/x/notes/9/#http-server)

- Up until this point, all HTML you saw was pre-written and static.
- In the past, when you visited a page, the browser downloaded an HTML page, and you were able to view it. These are considered _static_ pages, in that what is programmed in the HTML is exactly what the user sees and downloads _client-side_ to their internet browser.
- Dynamic pages refer to the ability of Python and similar languages to create HTML on-the-fly. Accordingly, you can have web pages that are generated _server-side_ by code based upon the input or behavior of users.
- You have used `http-server` in the past to serve your web pages. Today, we are going to utilize a new server that can parse out a web address and perform actions based on the URL provided.
- Further, last week, you saw URLs as follows:
    
    ```
    https://www.example.com/folder/file.html
    ```
    
    Notice that `file.html` is an HTML file inside a folder called `folder` at `example.com`.

## [Cookies and Session](https://cs50.harvard.edu/x/notes/9/#cookies-and-session)

- `app.py` is considered a _controller_. A _view_ is considered what the users see. A _model_ is how data is stored and manipulated. Together, this is referred to as _MVC_ (model, view, controller).
- While the prior implementation of `froshims` is useful from an administrative standpoint, where a back-office administrator could add and remove individuals from the database, one can imagine how this code is not safe to implement on a public server.
- For one, bad actors could make decisions on behalf of other users by hitting the deregister button – effectively deleting their recorded answer from the server.
- Web services like Google use login credentials to ensure users only have access to the right data.
- We can actually implement this itself using _cookies_. Cookies are small files that are stored on your computer such that your computer can communicate with the server and effectively say, “I’m an authorized user that has already logged in.” This authorization through this cookie is called a _session_.
- Cookies may be stored as follows:
    
    ```
    GET / HTTP/2
    Host: accounts.google.com
    Cookie: session=value
    ```
    
    Here, a `session` id is stored with a particular `value` representing that session.
    
- In the simplest form, we can implement this by creating a folder called `login` and then adding the following files.
- First, create a file called `requirements.txt` that reads as follows:
    
    ```
    Flask
    Flask-Session
    ```
    
    Notice that in addition to `Flask`, we also include `Flask-Session`, which is required to support login sessions.
    
- Second, in a `templates` folder, create a file called `layout.html` that appears as follows:
    
    ```
    <!DOCTYPE html>
    
    <html lang="en">
    
        <head>
            <meta name="viewport" content="initial-scale=1, width=device-width">
            <title>login</title>
        </head>
    
        <body>
            {% block body %}{% endblock %}
        </body>
    
    </html>
    ```
    
    Notice this provides a very simple layout with a title and a body.
    
- Third, create a file in the `templates` folder called `index.html` that appears as follows:
    
    ```
    {% extends "layout.html" %}
    
    {% block body %}
    
        {% if name -%}
            You are logged in as {{ name }}. <a href="/logout">Log out</a>.
        {%- else -%}
            You are not logged in. <a href="/login">Log in</a>.
        {%- endif %}
    
    {% endblock %}
    ```
    
    Notice that this file looks to see if `session["name"]` exists (elaborated further in `app.py` below). If it does, it will display a welcome message. If not, it will recommend you browse to a page to log in.
    
- Fourth, create a file called `login.html` and add the following code:
    
    ```
    {% extends "layout.html" %}
    
    {% block body %}
    
        <form action="/login" method="post">
            <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
            <button type="submit">Log In</button>
        </form>
    
    {% endblock %}
    ```
    
    Notice this is the layout of a basic login page.
    
- Finally, create a file called `app.py` and write code as follows:
    
    ```
    from flask import Flask, redirect, render_template, request, session
    from flask_session import Session
    
    # Configure app
    app = Flask(__name__)
    
    # Configure session
    app.config["SESSION_PERMANENT"] = False
    app.config["SESSION_TYPE"] = "filesystem"
    Session(app)
    
    
    @app.route("/")
    def index():
        return render_template("index.html", name=session.get("name"))
    
    
    @app.route("/login", methods=["GET", "POST"])
    def login():
        if request.method == "POST":
            session["name"] = request.form.get("name")
            return redirect("/")
        return render_template("login.html")
    
    
    @app.route("/logout")
    def logout():
        session.clear()
        return redirect("/")
    ```
    
    Notice the modified _imports_ at the top of the file, including `session`, which will allow you to support sessions. Most importantly, notice how `session["name"]` is used in the `login` and `logout` routes. The `login` route will assign the login name provided and assign it to `session["name"]`. However, in the `logout` route, the logging out is implemented by clearing the value of `session`.
    
- The `session` abstraction allows you to ensure only a specific user has access to specific data and features in our application. It allows you to ensure that no one acts on behalf of another user, for good or bad!
- If you wish, you can download [our implementation](https://cdn.cs50.net/2024/fall/lectures/9/src9/login/) of `login`.
- You can read more about sessions in the [Flask documentation](https://flask.palletsprojects.com/en/stable/api/#flask.session).












