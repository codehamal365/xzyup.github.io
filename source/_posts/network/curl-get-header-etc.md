---
uuid: bbaf4813-c0ab-11ec-92a1-7557b2313227
title: curl get
categories: Linux
tags:
  - curl
abbrlink: 3d76e967
---

# GET Request

## Send a GET Request and Print the Response to Screen

```bash
curl https://catonmat.net
```

You don't need to specify any arguments to make a GET request. It's curl's default request method. This recipe makes a GET request to `https://catonmat.net` and prints the returned content to screen.

## Send a GET Request and Save the Response to a File

```bash
curl -o response.txt https://catonmat.net
```

In this recipe, curl makes a GET request to `https://catonmat.net` and uses the `-o response.txt` argument to save the body of the HTTP response to `response.txt` file.

# Save the Response to a File

These curl recipes show you how to save the response from a curl request to a file. By default, curl prints the response to screen. To make it save the response to a file, use the `-o file` command line option.

Save the Response from a GET Request to a File

```bash
curl -o response.txt https://google.com?q=kitties
```

In this recipe, curl uses the `-o response.txt` command line option to save the response from a GET request that it makes to `https://google.com?q=kitties` to a file with filename `response.txt`.

## Use the Last Fragment of a URL as the Filename

```bash
curl -O https://catonmat.net/ftp/digg.pm
```

## Use > to store the content

~~~bash
curl -s https://domai -XPOST --data "$JSON_DATA" --header "Content-Type: application/json"  > result.json
~~~



# Construct a Query String 

This curl recipe shows you how to construct query strings for your GET requests. This is done via the `-G` command line argument in combination with the `-d` or `--data-urlencode` arguments. The `-G` argument will append the data specified in `-d` and `--data-urlencode` arguments at the end of the request URL, joining all data pieces with the `&` character and separating them from the URL with the `?` character.

### Construct Two Query Arguments

```bash
curl -G -d 'q=kitties' -d 'count=20' https://google.com/search
```

In this recipe, we let curl construct the query string and the final request URL for us. This recipe uses the `-G` option and the `-d` option twice that creates two query arguments. Curl joins them together like this `q=kitties&count=20` and appends this string at the end of the `https://google.com/search` request URL, and makes a GET request to `https://google.com/search?q=kitties&count=20`. Be careful – if you forget the `-G` argument, then curl will make a POST request instead!

### URL-encode a Query Argument

```bash
curl -G --data-urlencode 'comment=this cookbook is awesome' https://catonmat.net
```

This recipe uses the `--data-urlencode` argument. It works similar to the `-d` argument but curl also URL-encodes the value. In this recipe, the `comment` gets URL-encoded to `this%20cookbook%20is%20awesome` and the GET request goes to `https://catonmat.net?comment=this%20cookbook%20is%20awesome`.

# Add HTTP Headers

Last updated 1 week ago

These curl recipes show you how to add custom HTTP headers to curl requests. This is done via the `-H 'Header: Value'` command line argument.


## Add a Single Header

```bash
curl -H 'Accept-Language: en-US' https://google.com
```

This recipe uses the `-H` argument to add `Accept-Language: en-US` header to a GET request to `https://google.com`. This header tells Google to serve the English version of the page.

## Add Two Headers

```bash
curl -H 'Accept-Language: en-US' -H 'Secret-Message: xyzzy' https://google.com
```

This recipe adds two headers to a GET request to Google. The first header is the same as in the previous recipe and the other one is `Secret-Message: xyzzy`.

## Add an Empty Header

```bash
curl -H 'Puppies;' https://google.com
```

In this recipe, we add an empty header to a curl request. We pass `Puppies;` (with a semicolon at the end) as an argument to the `-H` option and curl converts it to an empty header `Puppies:` with no value.



## Use jq

~~~bash
curl -s --request POST 'https://$DOMAIN/auth/realms/main/protocol/openid-connect/token' --header 'Content-Type: application/x-www-form-urlencoded' --data-urlencode 'grant_type=client_credentials' --data-urlencode 'client_id=test' | jq -r .access_token)
~~~

---ess_token)
~~~

---