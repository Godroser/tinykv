实现独立存储
独立存储的接口
type Storage interface {
    // Other stuffs
    Write(ctx *kvrpcpb.Context, batch []Modify) error
    Reader(ctx *kvrpcpb.Context) (StorageReader, error)
}
我们主要需要在/kv/storage/standalone_storage/standalone/storage.go/中实现
Write(ctx kvrpcpb.Context，batch[]storage.Modify)
Reader(ctx kvrpcpb.Context)
Write(ctx kvrpcpb.Context，batch[]storage.Modify)将批量存储的修改写入物理存储，
Reader(ctx*kvrcpb.Context)创建迭代器以在物理存储中单独或迭代读取数据。
实现存储服务handler
具体来说，我们需要在/kv/server/raw_api中实现RawGet(), RawScan(), RawPut()和RawDelete(),使用在/kv/storage/standalone_storage/standalone_storage.go/中实现的方法执行。
