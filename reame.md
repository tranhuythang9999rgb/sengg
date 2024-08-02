protoc --proto_path=. --proto_path=googleapis --go_out=. --go-grpc_out=. apigrpc/apigrpc.proto
---
protoc --proto_path=. --proto_path=googleapis --go_out=./proto --go-grpc_out=./apigrpc proto/apigrpc.proto
---
--- sucess
protoc --proto_path=. --proto_path=googleapis --go_out=./proto --go-grpc_out=./proto proto/apigrpc.proto
---

protoc --proto_path=. --proto_path=googleapis \
  --go_out=. --go-grpc_out=. \
  --grpc-gateway_out ./proto --grpc-gateway_opt logtostderr=true \
  --grpc-gateway_opt paths=source_relative \
  proto/apigrpc.proto

--- sucess 2
protoc --proto_path=. --proto_path=googleapis --go_out=./proto --go-grpc_out=./proto --go_opt=Mproto/apigrpc.proto=/ proto/apigrpc.proto


proto-gateway:
protoc -I/usr/local/include -I. \
-I${GOPATH}/src \
-I${GOPATH}/src/github.com/grpc-ecosystem/grpc-gateway/third_party/googleapis \
--grpc-gateway_out=logtostderr=true,v=2:. \
proto/*.proto

cd proto
env PATH="$HOME/go/bin:$PATH" go generate -x ./...
cd proto
go generate -x ./...