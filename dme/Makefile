# Makefile

GOOGLEAPIS	= ../third_party/googleapis
INCLUDE		= -I. -I${GOOGLEAPIS} -I../edgeprotogen
BUILTIN		= Mgoogle/api/annotations.proto=${GOOGLEAPIS}/google/api,Mgoogle/protobuf/descriptor.proto=${GOOGLEAPIS}/google/protobuf,Medgeprotogen.proto=.,Mloc.proto=.,Mappcommon.proto=.,Mapp-client.proto=.,Mdynamic-location-group.proto=.
LASTTAG		= $(shell git describe --tags --abbrev=0)

# go install github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger@latest
doc:
	protoc ${INCLUDE} --swagger_out=logtostderr=true,allow_merge=true,merge_file_name=app-client:. *.proto

# Newer version of grpc-gateway and swagger generator
# go install github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2@latest
doc2:
	protoc ${INCLUDE} --openapiv2_out=${BUILTIN},logtostderr=true,allow_merge=true,merge_file_name=app-client:. *.proto

# Convert openapi v2 to v3
# https://npmjs.com/package/swagger2openapi
docv3: doc2
	swagger2openapi -o app-client-openapi.yaml -y app-client.swagger.json
