---
layout: post
title: Микросервисная архитектура онлайн-магазина: user-service
date: 2025-08-04
tags: [go, микросервисы, онлайн-магазин, highload, ddd, api-gateway, user-service]
---

# User-Service
Ну чтож давай начнем проектировать наш сервис.
За основу возьмем основную модель User
```go
type User struct {
	ID        int       `json:"id" db:"id"`
	Name      string    `json:"name" db:"name"`
	Email     string    `json:"email" db:"email"`
	CreatedAt time.Time `json:"created_at" db:"created_at"`
}
```

