# Makefile

GOOGLEAPIS	= ../third_party/googleapis
INCLUDE		= -I. -I${GOOGLEAPIS} -I../edgeprotogen
BUILTIN		= Mgoogle/api/annotations.proto=${GOOGLEAPIS}/google/api,Mgoogle/protobuf/descriptor.proto=${GOOGLEAPIS}/google/protobuf,Medgeprotogen.proto=.,Mloc.proto=.,Mappcommon.proto=.,Mapp-client.proto=.,Mdynamic-location-group.proto=.
LASTTAG		= $(shell git describe --tags --abbrev=0)

# Generate OpenAPI 3.0 and Swagger 2.0 api docs.
# go install github.com/google/gnostic/cmd/protoc-gen-openapi@latest
# go install github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger
doc:
	protoc ${INCLUDE} --openapi_out=${BUILTIN},version=${LASTTAG}:. *.proto
	protoc ${INCLUDE} --swagger_out=logtostderr=true,allow_merge=true,merge_file_name=app-client:. *.proto
