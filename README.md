# RxAlamofire

This is a fork of [RxAlamofire](https://github.com/RxSwiftCommunity/RxAlamofire/) 4.2.0.

I have added a hack to return a `DataResponseError` on error, so it's possible to get the `DataResponse` when an error occurs.

## Install pod

```
pod 'RxAlamofire', :git => 'https://github.com/fmaylinch/RxAlamofire.git', :tag => '4.2.0-DataResponseError'
```

## Example

```swift
RxAlamofire.data(method, url).subscribe(

  onError: { error in

    if let error = error as? DataResponseError<Data> {

      // Get response body (in this case, convert it to a String)
      if let data = error.response.data {
          let message = String(data: data, encoding: String.Encoding.utf8)
          print("Message: \(message)")
      }

      // Get status code
      if let statusCode = error.response.response?.statusCode {
          print("Status code: \(statusCode)")
      }
    }
  }
)
```
