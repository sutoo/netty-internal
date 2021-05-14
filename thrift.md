client视角

## TServiceClient
包含TProtocol。

client调用是交给 `TServiceClient`来处理的。

```
 class TServiceClient {
    protected TProtocol iprot_;
    protected TProtocol oprot_;
    protected int seqid_;
    protected void sendBase(String methodName, TBase<?, ?> args);
    protected void receiveBase(TBase<?, ?> result, String methodName);
    
    }
```
client端的一个XXXXX方法的同步接口的实现为：（依赖上面的TServiceClient的send/receive方法）
```
      send_XXXXXX(param);
      return recv_XXXXXX();
```

## TProtocol
包含TTransport。
protocol主要的接口为：write和read。
主要的实现：
TBinaryProtocol
TCompactProtocol （压缩）
TJSONProtocol

在protocol写的过程中，会不断的调用 trans的write方法。而不是一次性全部序列化好再写出。

## TTransport
各种实现，分别举例：
* THttpClient
写入ByteArrayOutputStream中，在flush时，发送http请求
* TNonblockingSocket
SocketChannel,写入后，不用flush
SocketChannel，
