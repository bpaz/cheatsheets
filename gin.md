---
title: Gin
layout: 2017/sheet
updated: 2017-11-27
category: golang
prism_languages: [go]
intro: > 
  [Gin](https://github.com/gin-gonic/gin) is a web framework written in Go (Golang).
---

## Install

{: .-no-hide}

```shell
 go get -u github.com/gin-gonic/gin
```

## Quick start

```go
package main

import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()
	r.GET("/ping", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "pong",
		})
	})
	r.Run() // listen and serve on 0.0.0.0:8080
}
```

---

## Routing

### Basic Example

```go
func main() {
	// Creates a gin router with default middleware:
	// logger and recovery (crash-free) middleware
	router := gin.Default()

	router.GET("/someGet", getting)
	router.POST("/somePost", posting)
	router.PUT("/somePut", putting)
	router.DELETE("/someDelete", deleting)
	router.PATCH("/somePatch", patching)
	router.HEAD("/someHead", head)
	router.OPTIONS("/someOptions", options)

	// By default it serves on :8080 unless a
	// PORT environment variable was defined.
	router.Run()
	// router.Run(":3000") for a hard coded port
}
```

### Parameters

#### Get Path parameters

```go
name := c.Param("name")
```

#### Get Query string

```go
firstname := c.DefaultQuery("firstname", "Guest")
```

### Responses

#### Success response

```go
c.JSON(http.StatusOK, gin.H{"status": "you are logged in"})
```

#### Error response

```go
 c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
 ```


## Model binding and validation

### Bind from JSON

```go
type Login struct {
	User     string `form:"user" json:"user" binding:"required"`
	Password string `form:"password" json:"password" binding:"required"`
}

func main() {
	// Example for binding JSON ({"user": "manu", "password": "123"})
	router.POST("/loginJSON", func(c *gin.Context) {
		var json Login
		if err := c.ShouldBindJSON(&json); err != nil {
			c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
			return
		}
		
		if json.User != "manu" || json.Password != "123" {
			c.JSON(http.StatusUnauthorized, gin.H{"status": "unauthorized"})
			return
		} 
		
		c.JSON(http.StatusOK, gin.H{"status": "you are logged in"})
	})
}
```

### Bind form

```go
type Login struct {
	User     string `form:"user" json:"user" binding:"required"`
	Password string `form:"password" json:"password" binding:"required"`
}

func main() {
    // Example for binding a HTML form (user=manu&password=123)
    router.POST("/loginForm", func(c *gin.Context) {
      var form Login
      // This will infer what binder to use depending on the content-type header.
      if err := c.ShouldBind(&form); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
          "error": err.Error()
        })
        return
      }
      
      if form.User != "manu" || form.Password != "123" {
        c.JSON(http.StatusUnauthorized, gin.H{
          "status":  "unauthorized"
        })
        return
      } 
      
      c.JSON(http.StatusOK, gin.H{"status": "you are logged in"})
    })
}
```  

References
----------

- <https://github.com/gin-gonic/gin>
