---
layout: post
title: nginx数据结构简介
categories: nginx
description: nginx数据结构简介
keywords: nginx
# topmost: true
---

# nginx数据结构

## ngx_str_t

```
typedef struct {
    size_t      len;
    u_char     *data;
} ngx_str_t;
```


1. ngx_str_t赋值方法1：
    ```
    #define ngx_string(str) { sizeof(str) - 1, (u_char *) str }
    ```

1. ngx_str_t赋值方法2：

    ```
    #define ngx_str_set(str, text)     \
        (str)->len = sizeof(text) - 1; \
        (str)->data = (u_char *)text
    ```



# FAQ

使用时多注意这些结构体（API）的用法。

* 注意sizeof()与ngx_strlen()相关的使用，否则使用出现各种坑。

* 采用ngx_str_t读取数据时，减少拷贝；

## atoi

教科书版的异常处理逻辑：
```
ngx_int_t
ngx_atoi(u_char *line, size_t n)
{
    ngx_int_t  value, cutoff, cutlim;

    if (n == 0) {
        return NGX_ERROR;
    }

    cutoff = NGX_MAX_INT_T_VALUE / 10;
    cutlim = NGX_MAX_INT_T_VALUE % 10;

    for (value = 0; n--; line++) {
        if (*line < '0' || *line > '9') {
            return NGX_ERROR;
        }

        if (value >= cutoff && (value > cutoff || *line - '0' > cutlim)) {
            return NGX_ERROR;
        }

        value = value * 10 + (*line - '0');
    }

    return value;
}
```

## 参考链接

- [https://stackoverflow.com/questions/26274518/ngx-str-set-truncating-value](https://stackoverflow.com/questions/26274518/ngx-str-set-truncating-value)