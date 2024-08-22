licenses(["notice"])

exports_files(["LICENSE"])

load("//bazel:braft.bzl", "braft_proto_library")

COPTS = [
    "-DBTHREAD_USE_FAST_PTHREAD_MUTEX",
    "-D__const__=__unused__",
    "-D_GNU_SOURCE",
    "-DUSE_SYMBOLIZE",
    "-DNO_TCMALLOC",
    "-D__STDC_FORMAT_MACROS",
    "-D__STDC_LIMIT_MACROS",
    "-D__STDC_CONSTANT_MACROS",
    "-DGFLAGS_NS=google",
] + select({
    "//bazel/config:brpc_with_glog": ["-DBRPC_WITH_GLOG=1"],
    "//conditions:default": ["-DBRPC_WITH_GLOG=0"],
}) + select({
    "//bazel/config:brpc_with_mesalink": ["-DUSE_MESALINK"],
    "//conditions:default": [""],
}) + select({
    "//bazel/config:brpc_with_thrift": ["-DENABLE_THRIFT_FRAMED_PROTOCOL=1"],
    "//conditions:default": [""],
}) + select({
    "//bazel/config:brpc_with_thrift_legacy_version": [],
    "//conditions:default": ["-DTHRIFT_STDCXX=std"],
}) + select({
    "//bazel/config:brpc_with_rdma": ["-DBRPC_WITH_RDMA=1"],
    "//conditions:default": [""],
})

LINKOPTS = [
    "-pthread",
    "-ldl",
] + select({
    "@bazel_tools//platforms:osx": [
        "-framework CoreFoundation",
        "-framework CoreGraphics",
        "-framework CoreData",
        "-framework CoreText",
        "-framework Security",
        "-framework Foundation",
        "-Wl,-U,_MallocExtension_ReleaseFreeMemory",
        "-Wl,-U,_ProfilerStart",
        "-Wl,-U,_ProfilerStop",
        "-Wl,-U,__Z13GetStackTracePPvii",
        "-Wl,-U,_RegisterThriftProtocol",
    ],
    "//conditions:default": [
        "-lrt",
    ],
}) + select({
    "//bazel/config:brpc_with_mesalink": [
        "-lmesalink",
    ],
    "//conditions:default": [],
}) + select({
    "//bazel/config:brpc_with_rdma": [
        "-libverbs",
    ],
    "//conditions:default": [],
})

cc_library(
    name = "braft",
    srcs = glob([
        "src/braft/*.cpp",
    ]),
    hdrs = glob([
        "src/braft/*.h",
    ]),
    includes = [
        "src",
    ],
    defines = [],
    copts = COPTS,
    linkopts = LINKOPTS,
    deps = [
        "@com_github_brpc_brpc//:brpc",
        "@com_github_gflags_gflags//:gflags",
        "@com_github_google_glog//:glog",
        "@com_google_protobuf//:protobuf",        
        ":cc_braft_internal_proto",
    ],
    visibility = ["//visibility:public"],
)

cc_binary(
    name = "counter_client",
    srcs = [
        "example/counter/client.cpp",
        ],
    copts = COPTS,
    linkopts = LINKOPTS,
    deps = [":braft",
            ":cc_example_counter_proto"],
)

cc_binary(
    name = "counter_server",
    srcs = [
        "example/counter/server.cpp",
        ],
    copts = COPTS,
    linkopts = LINKOPTS,
    deps = [":braft",
            ":cc_example_counter_proto"],
)

braft_proto_library(
    name = "cc_braft_internal_proto",
    srcs = glob([
        "src/braft/*.proto",
    ]),
    include = "src",
    visibility = ["//visibility:public"],
)

braft_proto_library(
    name = "cc_example_counter_proto",
    srcs = glob([
        "example/counter/*.proto",
    ]),
    include = "example/counter",
    visibility = ["//visibility:public"],
)
