# Makefile

GOOGLEAPIS	= ../third_party/googleapis
INCLUDE		= -I. -I${GOOGLEAPIS} -I../edgeprotogen
BUILTIN		= Mgoogle/api/annotations.proto=${GOOGLEAPIS}/google/api,Mgoogle/protobuf/descriptor.proto=${GOOGLEAPIS}/google/protobuf,Medgeprotogen.proto=.,Mloc.proto=.,Mappcommon.proto=.,Mapp-client.proto=.
LASTTAG		= $(shell git describe --tags --abbrev=0)

# go install github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2@latest
# https://npmjs.com/package/swagger2openapi
define gendoc-swagger
	protoc ${INCLUDE} --openapiv2_out=${BUILTIN},M$(1)=.,logtostderr=true,allow_merge=true,merge_file_name=$(basename $(1)):. $(1)
	swagger2openapi -o $(basename $(1)).yaml -y $(basename $(1)).swagger.json
endef

# Generate doc via swagger generation, then converting swagger to openapiv3
doc-swagger:
	$(call gendoc-swagger,app-client.proto)
	$(call gendoc-swagger,app-client-platos.proto)
	$(call gendoc-swagger,locverify.proto)
	$(call gendoc-swagger,qos.proto)
	$(call gendoc-swagger,qos-position.proto)
	$(call gendoc-swagger,session.proto)


# go install github.com/google/gnostic/cmd/protoc-gen-openapi@latest
define gendoc
	protoc ${INCLUDE} --openapi_out=${BUILTIN},M$(1)=.,naming=proto,enum_type=string,version=$(LASTTAG):. $(1)
	mv openapi.yaml $(basename $(1)).yaml
endef

# Generate doc directly from proto to openapiv3
doc:
	$(call gendoc,app-client.proto)
	$(call gendoc,session.proto)
