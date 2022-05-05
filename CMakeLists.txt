project(Protos_Example)
find_package(Protobuf REQUIRED)

include_directories(${PROTOBUF_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

file(GLOB ProtoFiles "${CMAKE_CURRENT_SOURCE_DIR}/*.proto")
PROTOBUF_GENERATE_CPP(PROTO_SRCS PROTO_HDRS ${ProtoFiles})
PROTOBUF_GENERATE_PYTHON(PROTO_PYS ${ProtoFiles})

add_library(Protos_Example ${PROTO_SRCS} ${PROTO_HDRS})
add_custom_target(proto_python ALL DEPENDS ${PROTO_PYS})

set(ProtobufMessagesIncludePath ${CMAKE_CURRENT_BINARY_DIR} PARENT_SCOPE)
