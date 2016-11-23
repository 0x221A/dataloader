# DataLoader
[![GoDoc](https://godoc.org/github.com/nicksrandall/dataloader?status.svg)](https://godoc.org/github.com/nicksrandall/dataloader)

This is an implementation of [Facebook's DataLoader](https://github.com/facebook/dataloader) in Golang.

## Status
This project is a work in progress. Feedback is encouraged.

## Examples
Coming soon. For now it may be helpful to look at the test file.

## Cache
This implementation contains a very basic cache that is intended only to be used for short lived DataLoaders (i.e. DataLoaders that ony exsist for the life of an http request). You may use your own implementation if you want.

## Usage
```go
// setup batch function
batchFn := func(keys []string) ([]dataloader.Result) {
  var results []dataloader.Result
  // do some aync work to get data for specified keys
  // append to this list resolved values
  return results
}
// Setup Cache (could be any cache that implements `Cache` interface
cache := dataloader.NewCache()
// create Loader
loader := dataloader.NewBatchedLoader(batchFn, time.Duration(16*time.Millisecond), cache, 0)

// Use loader
result := <- loader.load("key1")
if result.Error != nil {
  // handle data error
}

log.Printf("value: %#v", result.Data)
```
