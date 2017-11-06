# Alibaba Cloud STS SDK for Go

[![GitHub Version](https://badge.fury.io/gh/baiyubin%2Faliyun-sts-go-sdk.svg)](https://badge.fury.io/gh/baiyubin%2Faliyun-sts-go-sdk)
[![Build Status](https://travis-ci.org/baiyubin/aliyun-sts-go-sdk.svg?branch=master)](https://travis-ci.org/baiyubin/aliyun-sts-go-sdk)
[![Coverage Status](https://coveralls.io/repos/github/baiyubin/aliyun-sts-go-sdk/badge.svg?branch=master)](https://coveralls.io/github/baiyubin/aliyun-sts-go-sdk?branch=master)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](LICENSE)

## 关于
阿里云[STS](https://help.aliyun.com/document_detail/28756.html)(Security Token Service) 是为阿里云账号（或[RAM](https://help.aliyun.com/document_detail/28627.html)用户）提供短期访问权限管理的云服务。通过STS，您可以为联盟用户（您的本地账号系统所管理的用户）颁发一个自定义时效和访问权限的访问凭证。联盟用户可以使用STS短期访问凭证直接调用阿里云服务API，或登录阿里云管理控制台操作被授权访问的资源。

如果您需要快速掌握阿里云账号管理体系，请参看[云栖社区](https://yq.aliyun.com/articles/57895)。

## 版本
- 当前版本：1.0.0

## 运行环境
- Go 1.5及以上

## 安装方法
- 执行命令 `go get github.com/aliyun/aliyun-sts-go-sdk/sts`

## 使用方法
```go
package main

import (
	"fmt"
	"os"

	"github.com/aliyun/aliyun-sts-go-sdk/sts"
)

func handleError(err error) {
	fmt.Println(err)
	os.Exit(-1)
}

const (
	accessKeyID     = "<AccessKeyID>"
	accessKeySecret = "<AccessKeySecret>"
	roleArn         = "<RoleArn>"
	sessionName     = "sts_demo"
)

func main() {
	stsClient := sts.NewClient(accessKeyID, accessKeySecret, roleArn, sessionName)

	resp, err := stsClient.AssumeRole(3600)
	if err != nil {
		handleError(err)
	}

	fmt.Printf("Credentials:\n")
	fmt.Printf("    AccessKeyID:%s\n", resp.Credentials.AccessKeyId)
	fmt.Printf("    AccessKeySecret:%s\n", resp.Credentials.AccessKeySecret)
	fmt.Printf("    SecurityToken:%s\n", resp.Credentials.SecurityToken)
	fmt.Printf("    Expiration:%s\n", resp.Credentials.Expiration)
}
```

## 作者
- [Yubin Bai](https://github.com/baiyubin)

## 协议
- [MIT](https://github.com/aliyun/aliyun-sts-go-sdk/blob/master/LICENSE)
