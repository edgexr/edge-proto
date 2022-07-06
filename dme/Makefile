# Makefile

GOOGLEAPIS	= ../third_party/googleapis
INCLUDE		= -I. -I${GOOGLEAPIS} -I../edgeprotogen
BUILTIN		= Mgoogle/api/annotations.proto=${GOOGLEAPIS}/google/api,Mgoogle/protobuf/descriptor.proto=${GOOGLEAPIS}/google/protobuf,Medgeprotogen.proto=.,Mloc.proto=.,Mappcommon.proto=.

# go install github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2@latest
# https://npmjs.com/package/swagger2openapi
define gendoc
	protoc ${INCLUDE} --openapiv2_out=${BUILTIN},M$(1)=.,logtostderr=true,allow_merge=true,merge_file_name=$(basename $(1)):. $(1)
	swagger2openapi -o $(basename $(1)).yaml -y $(basename $(1)).swagger.json
endef

doc:
	$(call gendoc,app-client.proto)
	$(call gendoc,locverify.proto)
	$(call gendoc,qos.proto)
	$(call gendoc,qos-position.proto)
	$(call gendoc,session.proto)
