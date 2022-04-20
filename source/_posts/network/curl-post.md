---
title: cur post
tags:
  - curl
abbrlink: '25e6'
---

# POST Request

## Send an Empty POST Request

```bash
curl -X POST https://catonmat.net
```

This recipe uses the `-X POST` option that makes curl send a POST request to `https://catonmat.net`. Once it receives a response from the server, it prints the response body to the screen. It doesn't send any POST data.

## Send a POST Request with Form Data

```bash
curl -d 'login=emma&password=123' -X POST https://google.com/login
```

This recipe sends a POST request to `https://google.com/login` with `login=emma&password=123` data in request's body. When using the `-d` argument, curl also sets the `Content-Type` header to `application/x-www-form-urlencoded`. Additionally, when the `-d` option is set, the `-X POST` argument can be skipped as curl will automatically set the request's type to POST.

## Skipping the -X Argument

```bash
curl -d 'login=emma&password=123' https://google.com/login
```

In this recipe, we skip the `-X POST` argument that explicitly tells curl to send a POST request. We can skip it because we have specified the `-d` argument. When `-d` is used, curl implicitly sets the request's type to POST.

## A Neater Way to POST Data

```bash
curl -d 'login=emma' -d 'password=123' https://google.com/login
```

The previous recipe used a single `-d` option to send all data `login=emma&password=123` but here's a neater way to do the same that makes the command easier to read. Instead of using a single `-d` argument for all data, use multiple `-d` arguments for each `key=value` data piece! If you do that, then curl joins all data pieces with the `&` separator symbol when creating the request. This recipe skips the `-X POST` argument because when `-d` argument is present, curl makes a POST request implicitly.

## Send a POST Request and Follow a Redirect

```bash
curl -L -d 'tweet=hi' https://api.twitter.com/tweet
```

This recipe uses the `-L` command line option that tells curl to follow any possible redirects that it may encounter in the way. By default, curl doesn't follow the redirects, so you have to add `-L` to make it follow them. This recipe skips the `-X POST` argument because `-d` argument forces curl to make a POST request.

## Send a POST Request with JSON Data

```bash
curl -d '{"login": "emma", "pass": "123"}' -H 'Content-Type: application/json' https://google.com/login
```

In this recipe, curl sends a POST request with JSON data in it. This is accomplished by passing JSON to the `-d` option and also using the `-H` option that sets the `Content-Type` header to `application/json`. Setting the content type header to `application/json` is necessary because otherwise, the web server won't know what type of data this is. I've also removed the `-X POST` argument as it can be skipped because `-d` forces a POST request.

## Send a POST Request with XML Data

```bash
curl -d '<user><login>ann</login><password>123</password></user>' -H 'Content-Type: text/xml' https://google.com/login
```

This recipe POSTs XML data to `https://google.com/login`. Just like the form data and JSON data, XML data is specified in the `-d` argument. To tell the web server that the request contains XML, the `Content-Type` header is changed to `text/xml` via the `-H` argument.

## Send a POST Request with Plain Text Data

```bash
curl -d 'hello world' -H 'Content-Type: text/plain' https://google.com/login
```

This recipe sends a POST request with a plain text string `hello world` in request's body. It also sets the `Content-Type` header to `text/plain` to tell web server that it's just plain text coming in.

## Send a POST Request with Data from a File

```bash
curl -d '@data.txt' https://google.com/login
```

This recipe loads POST data from a file called `data.txt`. Notice the extra `@` symbol before the filename. That's how you tell curl that `data.txt` is a file and not just a string that should go in the POST body.

## URL-encode POST Data

```bash
curl --data-urlencode 'comment=hello world' https://google.com/login
```

So far, all recipes have been using the `-d` argument to add POST data to requests. This argument assumes that your data is URL-encoded already. If it is not, then there can be some trouble. If your data is not URL-encoded, then replace `-d` with `--data-urlencode`. It works exactly the same way as `-d`, except the data gets URL-encoded by curl before it's sent out on the wire.

## POST a Binary File

```
curl -F 'file=@photo.png' https://google.com/profile
```

This recipe uses the `-F` argument that forces curl to make a multipart form data POST request. It's a more complicated content type that's more efficient at sending binary files. This recipe makes curl read an image `photo.png` and upload it to `https://google.com/profile` with a name `file`. The `-F` argument also sets the `Content-Type` header to `multipart/form-data`.

## POST a Binary File and Set Its MIME Type

```
curl -F 'file=@photo.png;type=image/png' https://google.com/profile
```

Similar to the previous recipe, this recipe uses the `-F` argument to upload a binary file (a photo with the filename `photo.png`) via a multipart POST request. It also specifies the MIME type of this file and sets it to `image/png`. If no type is specified, then curl sets it to `application/octet-stream`.

## POST a Binary File and Change Its Filename

```
curl -F 'file=@photo.png;filename=me.png' https://google.com/profile
```

Similar to the previous two recipes, this recipe uses the `-F` argument to upload a `photo.png` via a POST request. Additionally, in this recipe, the filename that is sent to the web server is changed from `photo.png` to `me.png`. The web server only sees the filename `me.png` and doesn't know the original filename was `photo.png`.

# Add POST Data to a Request

Last updated 1 week ago

These curl recipes show you how to add POST data to curl requests. To add URL-encoded form data, use the `-d` argument. To make curl URL-escape form data for you, use the `--data-urlencode` argument. To send multipart form data, use the `-F` argument.


## Send Form Data

```
curl -d 'name=johnny%20depp' https://google.com/login
```

This recipe uses the `-d` argument to add `name=johnny%20depp` to the body of a POST request to `https://google.com/login`. When using the `-d` argument, curl automatically adds the `Content-Type: application/x-www-form-urlencoded` header that tells the web server it's sending URL-encoded form data. Note that the `key=value` data should be URL-escaped.

## URL-encode and Send Form Data

```
curl --data-urlencode 'name=john depp' https://google.com/login
```

This recipe uses the `--data-urlencode` argument to add `name=john depp` form data to a POST request. This argument works just like the `-d` argument in the previous recipe, except it also URL-encodes the data. Thus, the data this recipe adds to the body of the POST request is `name=johnny%20depp` and the request is then sent to `https://google.com/login`.

## Using Multiple -d Arguments

```
curl -d 'foo=bar' -d 'baz=quux' https://google.com
```

The previous two recipes sent just a single variable in the POST request but you can send as many variables as you need. Just specify them one after another. This recipe POSTs two variables, `foo=bar` and `baz=quux`.

## Send Multipart Data

```
curl -F 'name=johnny' https://google.com/search
```

This recipe uses the `-F` argument to send multipart form data in a POST request. When sending multipart data, curl sets the `Content-Type` header to `multipart/form-data`. Sending multipart data is useful when you need to upload images or other binary files.

## Upload an Image

```
curl -F 'pic=@me.jpg' https://google.com/profile
```

This recipe also uses the `-F` argument but instead of sending textual data, it sends the file `me.jpg`. It uploads it to `https://google.com/profile` via a POST request. As this recipe uses the `-F` argument, this image is uploaded as multipart base64-encoded form data.

## Upload an Image and Change Its Filename

```
curl -F 'pic=@me.jpg;filename=x.jpg' https://google.com/profile
```

This recipe adds a special argument `filename=x.jpg` after `me.jpg`. This tells curl to use a new filename for the attached file. Curl will read `me.jpg` but tell the server that the filename is `x.jpg`.

## Send JSON Data

```
curl -H 'Content-Type: application/json' -d '{"query": "cats"}' https://google.com/search
```

This recipe sends a POST request with JSON data in it. It specifies the JSON data itself as the argument to the `-d` switch, and it also sets the request's content type to `application/json` via the `-H` argument so that the web server knew that the incoming data is JSON and not plain text.

## Send XML Data

```
curl -H 'Content-Type: text/xml' -d 'hello' https://google.com/msg
```

This recipe sets the content type header to `text/xml`, which is the MIME type of XML. It then adds `<message>hello</message>` data to the request and POSTs it to `https://google.com/msg`. Sending XML data, JSON data, or any other text data is very similar. All you have to do is change the content type header to the correct MIME type so that the server and the application know what type of data it is.

---