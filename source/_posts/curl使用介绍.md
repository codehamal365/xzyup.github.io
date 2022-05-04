---
uuid: bbaf4815-c0ab-11ec-92a1-7557b2313227
title: cur参数
categories: Linux
tags:
  - curl
abbrlink: 44f7453a
---

# 简介

curl 是常用的命令行工具，用来请求 Web 服务器。它的名字就是客户端（client）的 URL 工具的意思。

它的功能非常强大，命令行参数多达几十种。如果熟练的话，完全可以取代 Postman 这一类的图形界面工具。

参考：[curl cookbook](https://catonmat.net/cookbooks/curl)

## 常用命令

不带有任何参数时，curl 就是发出 GET 请求。

~~~bash
curl https://www.baidu.com
~~~

以上命令向`www.baidu.com`发出GET请求，服务器返回的内容会在命令行输出。

### -A

`-A`参数指定客户端的用户代理标头，即`User—Agent`。curl的默认用户代理字符串是`curl/[version]`。

~~~bash
curl -A 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.100 Safari/537.36' https://google.com
~~~

上面的命令将`User-Agent`改成Chrome浏览器。

~~~bash
curl -A '' https://google.com
~~~

上面命令会移除`User-Agent`标头。也可以通过`-H`参数直接指定标头，更改`User-Agent`。

~~~bash
curl -H 'User-Agent: php/1.0' https://google.com
~~~

### -b

`-b`参数用来向服务器发送 Cookie。

~~~bash
curl -b 'foo=bar' https://google.com
~~~

上面命令会生成一个标头`Cookie: foo=bar`，向服务器发送一个名为`foo`、值为`bar`的 Cookie。

```bash
 curl -b 'foo1=bar;foo2=bar2' https://google.com
```

上面命令发送两个 Cookie。

```bash
curl -b cookies.txt https://www.google.com
```

上面命令读取本地文件`cookies.txt`，里面是服务器设置的 Cookie（参见`-c`参数），将其发送到服务器。

### -c

`-c`参数将服务器设置的 Cookie 写入一个文件。

```bash
curl -c cookies.txt https://www.google.com
```

上面命令将服务器的 HTTP 回应所设置 Cookie 写入文本文件`cookies.txt`。

### -d

`-d`参数用于发送 POST 请求的数据体。

```bash
$ curl -d 'login=emma＆password=123'-X POST https://google.com/login
# 或者
$ curl -d 'login=emma' -d 'password=123' -X POST  https://google.com/login
```

使用`-d`参数以后，HTTP 请求会自动加上标头`Content-Type : application/x-www-form-urlencoded`。并且会自动将请求转为 POST 方法，因此可以省略`-X POST`。

`-d`参数可以读取本地文本文件的数据，向服务器发送。

```bash
 curl -d '@data.txt' https://google.com/login
```

上面命令读取`data.txt`文件的内容，作为数据体向服务器发送。

### **--data-urlencode**

`--data-urlencode`参数等同于`-d`，发送 POST 请求的数据体，区别在于会自动将发送的数据进行 URL 编码。

```bash
curl --data-urlencode 'comment=hello world' https://google.com/login
```

上面代码中，发送的数据`hello world`之间有一个空格，需要进行 URL 编码。

### -e

`-e`参数用来设置 HTTP 的标头`Referer`，表示请求的来源。

```bash
curl -e 'https://google.com?q=example' https://www.example.com
```

上面命令将`Referer`标头设为`https://google.com?q=example`。

`-H`参数可以通过直接添加标头`Referer`，达到同样效果。

```bash
curl -H 'Referer: https://google.com?q=example' https://www.example.com
```

### -F

`-F`参数用来向服务器上传二进制文件。

```bash
curl -F 'file=@photo.png' https://google.com/profile
```

上面命令会给 HTTP 请求加上标头`Content-Type: multipart/form-data`，然后将文件`photo.png`作为`file`字段上传。

`-F`参数可以指定 MIME 类型。

```bash
curl -F 'file=@photo.png;type=image/png' https://google.com/profile
```

上面命令指定 MIME 类型为`image/png`，否则 curl 会把 MIME 类型设为`application/octet-stream`。

`-F`参数也可以指定文件名。

```bash
curl -F 'file=@photo.png;filename=me.png' https://google.com/profile
```

上面命令中，原始文件名为`photo.png`，但是服务器接收到的文件名为`me.png`。

### **-G**

`-G`参数用来构造 URL 的查询字符串。

```bash
curl -G -d 'q=kitties' -d 'count=20' https://google.com/search
```

上面命令会发出一个 GET 请求，实际请求的 URL 为`https://google.com/search?q=kitties&count=20`。如果省略`--G`，会发出一个 POST 请求。

如果数据需要 URL 编码，可以结合`--data--urlencode`参数。

```bash
curl -G --data-urlencode 'comment=hello world' https://www.example.com
```

### **-H**

`-H`参数添加 HTTP 请求的标头。

```bash
curl -H 'Accept-Language: en-US' https://google.com
```

上面命令添加 HTTP 标头`Accept-Language: en-US`。

```bash
curl -H 'Accept-Language: en-US' -H 'Secret-Message: xyzzy' https://google.com
```

上面命令添加两个 HTTP 标头。

```bash
curl -d '{"login": "emma", "pass": "123"}' -H 'Content-Type: application/json' https://google.com/login
```

上面命令添加 HTTP 请求的标头是`Content-Type: application/json`，然后用`-d`参数发送 JSON 数据。

### **-i**

`-i`参数打印出服务器回应的 HTTP 标头。

```bash
curl -i https://www.example.com
```

上面命令收到服务器回应后，先输出服务器回应的标头，然后空一行，再输出网页的源码。

### **-I**

`-I`参数向服务器发出 HEAD 请求，然会将服务器返回的 HTTP 标头打印出来。

```bash
 curl -I https://www.example.com
```

上面命令输出服务器对 HEAD 请求的回应。

`--head`参数等同于`-I`。

```bash
curl --head https://www.example.com
```

### **-k**

`-k`参数指定跳过 SSL 检测。

```bash
curl -k https://www.example.com
```

上面命令不会检查服务器的 SSL 证书是否正确。

### **-L**

`-L`参数会让 HTTP 请求跟随服务器的重定向。curl 默认不跟随重定向。

```bash
curl -L -d 'tweet=hi' https://api.twitter.com/tweet
```

### **--limit-rate**

`--limit-rate`用来限制 HTTP 请求和回应的带宽，模拟慢网速的环境。

```bash
curl --limit-rate 200k https://google.com
```

上面命令将带宽限制在每秒 200K 字节。

### **-o**

`-o`参数将服务器的回应保存成文件，等同于`wget`命令。

```bash
curl -o example.html https://www.example.com
```

### **-O**

`-O`参数将服务器回应保存成文件，并将 URL 的最后部分当作文件名。

```bash
curl -O https://www.example.com/foo/bar.html
```

上面命令将服务器回应保存成文件，文件名为`bar.html`。

### -s

`-s`参数将不输出错误和进度信息。

```bash
curl -s https://www.example.com
```

上面命令一旦发生错误，不会显示错误信息。不发生错误的话，会正常显示运行结果。

如果想让 curl 不产生任何输出，可以使用下面的命令。

```bash
curl -s -o /dev/null https://google.com
```

### **-S**

`-S`参数指定只输出错误信息，通常与`-s`一起使用。

```bash
curl -s -o /dev/null https://google.com
```

上面命令没有任何输出，除非发生错误。

### **-u**

`-u`参数用来设置服务器认证的用户名和密码。

```bash
curl -u 'bob:12345' https://google.com/login
```

上面命令设置用户名为`bob`，密码为`12345`，然后将其转为 HTTP 标头`Authorization: Basic Ym9iOjEyMzQ1`。

curl 能够识别 URL 里面的用户名和密码。

```bash
curl https://bob:12345@google.com/login
```

上面命令能够识别 URL 里面的用户名和密码，将其转为上个例子里面的 HTTP 标头。

```bash
curl -u 'bob' https://google.com/login
```

上面命令只设置了用户名，执行后，curl 会提示用户输入密码。

### **-v**

`-v`参数输出通信的整个过程，用于调试。

```bash
curl -v https://www.example.com
```

`--trace`参数也可以用于调试，还会输出原始的二进制数据。

```bash
curl --trace - https://www.example.com
```

### **-x**

`-x`参数指定 HTTP 请求的代理。

```bash
curl -x socks5://james:cats@myproxy.com:8080 https://www.example.com
```

上面命令指定 HTTP 请求通过`myproxy.com:8080`的 socks5 代理发出。

如果没有指定代理协议，默认为 HTTP。

```bash
 curl -x james:cats@myproxy.com:8080 https://www.example.com
```

上面命令中，请求的代理使用 HTTP 协议。

### **-X**

`-X`参数指定 HTTP 请求的方法。

```bash
curl -X POST https://www.example.com
```

上面命令对`https://www.example.com`发出 POST 请求。



## GET请求

### Send a GET Request and Print the Response to Screen

```bash
curl https://catonmat.net
```

You don't need to specify any arguments to make a GET request. It's curl's default request method. This recipe makes a GET request to `https://catonmat.net` and prints the returned content to screen.

### Send a GET Request and Save the Response to a File

```bash
curl -o response.txt https://catonmat.net
```

In this recipe, curl makes a GET request to `https://catonmat.net` and uses the `-o response.txt` argument to save the body of the HTTP response to `response.txt` file.

### Save the Response to a File

These curl recipes show you how to save the response from a curl request to a file. By default, curl prints the response to screen. To make it save the response to a file, use the `-o file` command line option.

Save the Response from a GET Request to a File

```bash
curl -o response.txt https://google.com?q=kitties
```

In this recipe, curl uses the `-o response.txt` command line option to save the response from a GET request that it makes to `https://google.com?q=kitties` to a file with filename `response.txt`.

#### Use the Last Fragment of a URL as the Filename

```bash
curl -O https://catonmat.net/ftp/digg.pm
```

### Use > to store the content

~~~bash
curl -s https://domai -XPOST --data "$JSON_DATA" --header "Content-Type: application/json"  > result.json
~~~

### Construct a Query String 

This curl recipe shows you how to construct query strings for your GET requests. This is done via the `-G` command line argument in combination with the `-d` or `--data-urlencode` arguments. The `-G` argument will append the data specified in `-d` and `--data-urlencode` arguments at the end of the request URL, joining all data pieces with the `&` character and separating them from the URL with the `?` character.

#### Construct Two Query Arguments

```bash
curl -G -d 'q=kitties' -d 'count=20' https://google.com/search
```

In this recipe, we let curl construct the query string and the final request URL for us. This recipe uses the `-G` option and the `-d` option twice that creates two query arguments. Curl joins them together like this `q=kitties&count=20` and appends this string at the end of the `https://google.com/search` request URL, and makes a GET request to `https://google.com/search?q=kitties&count=20`. Be careful – if you forget the `-G` argument, then curl will make a POST request instead!

#### URL-encode a Query Argument

```bash
curl -G --data-urlencode 'comment=this cookbook is awesome' https://catonmat.net
```

This recipe uses the `--data-urlencode` argument. It works similar to the `-d` argument but curl also URL-encodes the value. In this recipe, the `comment` gets URL-encoded to `this%20cookbook%20is%20awesome` and the GET request goes to `https://catonmat.net?comment=this%20cookbook%20is%20awesome`.

### Add HTTP Headers

These curl recipes show you how to add custom HTTP headers to curl requests. This is done via the `-H 'Header: Value'` command line argument.

#### Add a Single Header

```bash
curl -H 'Accept-Language: en-US' https://google.com
```

This recipe uses the `-H` argument to add `Accept-Language: en-US` header to a GET request to `https://google.com`. This header tells Google to serve the English version of the page.

#### Add Two Headers

```bash
curl -H 'Accept-Language: en-US' -H 'Secret-Message: xyzzy' https://google.com
```

This recipe adds two headers to a GET request to Google. The first header is the same as in the previous recipe and the other one is `Secret-Message: xyzzy`.

#### Add an Empty Header

```bash
curl -H 'Puppies;' https://google.com
```

In this recipe, we add an empty header to a curl request. We pass `Puppies;` (with a semicolon at the end) as an argument to the `-H` option and curl converts it to an empty header `Puppies:` with no value.

#### Use jq

~~~bash
curl -s --request POST 'https://$DOMAIN/auth/realms/main/protocol/openid-connect/token' --header 'Content-Type: application/x-www-form-urlencoded' --data-urlencode 'grant_type=client_credentials' --data-urlencode 'client_id=test' | jq -r .access_token)
~~~



## POST请求

### Send an Empty POST Request

```bash
curl -X POST https://catonmat.net
```

This recipe uses the `-X POST` option that makes curl send a POST request to `https://catonmat.net`. Once it receives a response from the server, it prints the response body to the screen. It doesn't send any POST data.

### Send a POST Request with Form Data

```bash
curl -d 'login=emma&password=123' -X POST https://google.com/login
```

This recipe sends a POST request to `https://google.com/login` with `login=emma&password=123` data in request's body. When using the `-d` argument, curl also sets the `Content-Type` header to `application/x-www-form-urlencoded`. Additionally, when the `-d` option is set, the `-X POST` argument can be skipped as curl will automatically set the request's type to POST.

### Skipping the -X Argument

```bash
curl -d 'login=emma&password=123' https://google.com/login
```

In this recipe, we skip the `-X POST` argument that explicitly tells curl to send a POST request. We can skip it because we have specified the `-d` argument. When `-d` is used, curl implicitly sets the request's type to POST.

### A Neater Way to POST Data

```bash
curl -d 'login=emma' -d 'password=123' https://google.com/login
```

The previous recipe used a single `-d` option to send all data `login=emma&password=123` but here's a neater way to do the same that makes the command easier to read. Instead of using a single `-d` argument for all data, use multiple `-d` arguments for each `key=value` data piece! If you do that, then curl joins all data pieces with the `&` separator symbol when creating the request. This recipe skips the `-X POST` argument because when `-d` argument is present, curl makes a POST request implicitly.

### Send a POST Request and Follow a Redirect

```bash
curl -L -d 'tweet=hi' https://api.twitter.com/tweet
```

This recipe uses the `-L` command line option that tells curl to follow any possible redirects that it may encounter in the way. By default, curl doesn't follow the redirects, so you have to add `-L` to make it follow them. This recipe skips the `-X POST` argument because `-d` argument forces curl to make a POST request.

### Send a POST Request with JSON Data

```bash
curl -d '{"login": "emma", "pass": "123"}' -H 'Content-Type: application/json' https://google.com/login
```

In this recipe, curl sends a POST request with JSON data in it. This is accomplished by passing JSON to the `-d` option and also using the `-H` option that sets the `Content-Type` header to `application/json`. Setting the content type header to `application/json` is necessary because otherwise, the web server won't know what type of data this is. I've also removed the `-X POST` argument as it can be skipped because `-d` forces a POST request.

### Send a POST Request with XML Data

```bash
curl -d '<user><login>ann</login><password>123</password></user>' -H 'Content-Type: text/xml' https://google.com/login
```

This recipe POSTs XML data to `https://google.com/login`. Just like the form data and JSON data, XML data is specified in the `-d` argument. To tell the web server that the request contains XML, the `Content-Type` header is changed to `text/xml` via the `-H` argument.

### Send a POST Request with Plain Text Data

```bash
curl -d 'hello world' -H 'Content-Type: text/plain' https://google.com/login
```

This recipe sends a POST request with a plain text string `hello world` in request's body. It also sets the `Content-Type` header to `text/plain` to tell web server that it's just plain text coming in.

### Send a POST Request with Data from a File

```bash
curl -d '@data.txt' https://google.com/login
```

This recipe loads POST data from a file called `data.txt`. Notice the extra `@` symbol before the filename. That's how you tell curl that `data.txt` is a file and not just a string that should go in the POST body.

### URL-encode POST Data

```bash
curl --data-urlencode 'comment=hello world' https://google.com/login
```

So far, all recipes have been using the `-d` argument to add POST data to requests. This argument assumes that your data is URL-encoded already. If it is not, then there can be some trouble. If your data is not URL-encoded, then replace `-d` with `--data-urlencode`. It works exactly the same way as `-d`, except the data gets URL-encoded by curl before it's sent out on the wire.

### POST a Binary File

```
curl -F 'file=@photo.png' https://google.com/profile
```

This recipe uses the `-F` argument that forces curl to make a multipart form data POST request. It's a more complicated content type that's more efficient at sending binary files. This recipe makes curl read an image `photo.png` and upload it to `https://google.com/profile` with a name `file`. The `-F` argument also sets the `Content-Type` header to `multipart/form-data`.

### POST a Binary File and Set Its MIME Type

```
curl -F 'file=@photo.png;type=image/png' https://google.com/profile
```

Similar to the previous recipe, this recipe uses the `-F` argument to upload a binary file (a photo with the filename `photo.png`) via a multipart POST request. It also specifies the MIME type of this file and sets it to `image/png`. If no type is specified, then curl sets it to `application/octet-stream`.

### POST a Binary File and Change Its Filename

```
curl -F 'file=@photo.png;filename=me.png' https://google.com/profile
```

Similar to the previous two recipes, this recipe uses the `-F` argument to upload a `photo.png` via a POST request. Additionally, in this recipe, the filename that is sent to the web server is changed from `photo.png` to `me.png`. The web server only sees the filename `me.png` and doesn't know the original filename was `photo.png`.

### Add POST Data to a Request

These curl recipes show you how to add POST data to curl requests. To add URL-encoded form data, use the `-d` argument. To make curl URL-escape form data for you, use the `--data-urlencode` argument. To send multipart form data, use the `-F` argument.

#### Send Form Data

```
curl -d 'name=johnny%20depp' https://google.com/login
```

This recipe uses the `-d` argument to add `name=johnny%20depp` to the body of a POST request to `https://google.com/login`. When using the `-d` argument, curl automatically adds the `Content-Type: application/x-www-form-urlencoded` header that tells the web server it's sending URL-encoded form data. Note that the `key=value` data should be URL-escaped.

#### URL-encode and Send Form Data

```
curl --data-urlencode 'name=john depp' https://google.com/login
```

This recipe uses the `--data-urlencode` argument to add `name=john depp` form data to a POST request. This argument works just like the `-d` argument in the previous recipe, except it also URL-encodes the data. Thus, the data this recipe adds to the body of the POST request is `name=johnny%20depp` and the request is then sent to `https://google.com/login`.

#### Using Multiple -d Arguments

```
curl -d 'foo=bar' -d 'baz=quux' https://google.com
```

The previous two recipes sent just a single variable in the POST request but you can send as many variables as you need. Just specify them one after another. This recipe POSTs two variables, `foo=bar` and `baz=quux`.

### Send Multipart Data

```
curl -F 'name=johnny' https://google.com/search
```

This recipe uses the `-F` argument to send multipart form data in a POST request. When sending multipart data, curl sets the `Content-Type` header to `multipart/form-data`. Sending multipart data is useful when you need to upload images or other binary files.

### Upload an Image

```
curl -F 'pic=@me.jpg' https://google.com/profile
```

This recipe also uses the `-F` argument but instead of sending textual data, it sends the file `me.jpg`. It uploads it to `https://google.com/profile` via a POST request. As this recipe uses the `-F` argument, this image is uploaded as multipart base64-encoded form data.

### Upload an Image and Change Its Filename

```
curl -F 'pic=@me.jpg;filename=x.jpg' https://google.com/profile
```

This recipe adds a special argument `filename=x.jpg` after `me.jpg`. This tells curl to use a new filename for the attached file. Curl will read `me.jpg` but tell the server that the filename is `x.jpg`.

### Send JSON Data

```
curl -H 'Content-Type: application/json' -d '{"query": "cats"}' https://google.com/search
```

This recipe sends a POST request with JSON data in it. It specifies the JSON data itself as the argument to the `-d` switch, and it also sets the request's content type to `application/json` via the `-H` argument so that the web server knew that the incoming data is JSON and not plain text.

### Send XML Data

```
curl -H 'Content-Type: text/xml' -d 'hello' https://google.com/msg
```

This recipe sets the content type header to `text/xml`, which is the MIME type of XML. It then adds `<message>hello</message>` data to the request and POSTs it to `https://google.com/msg`. Sending XML data, JSON data, or any other text data is very similar. All you have to do is change the content type header to the correct MIME type so that the server and the application know what type of data it is.
