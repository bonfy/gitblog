# [Go 中 interface 类似 Python DuckType 的用法](https://github.com/bonfy/gitblog/issues/7)

```go
package main

import "fmt"

type Downloader interface {
	Download(url string)
}

type BaiduDownloader struct {
}

func (BaiduDownloader) Download(url string) {
	fmt.Println("Download Baidu:", url)
}

type YoukuDownloader struct {
}

func (YoukuDownloader) Download(url string) {
	fmt.Println("Download Youku:", url)
}

func Process(url string, d Downloader) {
	d.Download(url)
}

func main() {
	url := "youku-url"
	Process(url, YoukuDownloader{})
	url = "baidu-url"
	Process(url, BaiduDownloader{})
}
```