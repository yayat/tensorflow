# Libraries and Kernels for Linear Optimization.

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

package(default_visibility = ["//tensorflow:__subpackages__"])

load("//tensorflow:tensorflow.bzl", "tf_cc_test")
load(
    "//tensorflow/core:platform/default/build_config.bzl",
    "tf_kernel_tests_linkstatic",
)

cc_library(
    name = "loss_updaters",
    hdrs = [
        "hinge-loss.h",
        "logistic-loss.h",
        "loss.h",
        "squared-loss.h",
    ],
    deps = [
        "@protobuf//:protobuf",
        "//tensorflow/core:framework_headers_lib",
    ],
)

cc_test(
    name = "loss_test",
    size = "small",
    srcs = ["loss_test.cc"],
    deps = [
        ":loss_updaters",
        "//tensorflow/core:lib",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
    ],
)

cc_library(
    name = "resources",
    srcs = ["resources.cc"],
    hdrs = ["resources.h"],
    deps = [
        "@protobuf//:protobuf",
        "//tensorflow/core:framework_headers_lib",
        "//third_party/eigen3",
    ],
)

cc_test(
    name = "resources_test",
    size = "small",
    srcs = ["resources_test.cc"],
    deps = [
        ":resources",
        "//tensorflow/core:framework",
        "//tensorflow/core:lib",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
    ],
)

cc_library(
    name = "sdca_ops",
    srcs = ["sdca_ops.cc"],
    deps = [
        ":loss_updaters",
        ":resources",
        "@protobuf//:protobuf",
        "//tensorflow/core:framework_headers_lib",
        "//tensorflow/core/kernels:bounds_check_lib",
        "//third_party/eigen3",
    ],
    alwayslink = 1,
)

tf_cc_test(
    name = "sdca_ops_test",
    size = "small",
    linkstatic = tf_kernel_tests_linkstatic(),  # Required for benchmarking
    deps = [
        "//tensorflow/contrib/linear_optimizer:sdca_op_kernels",
        "//tensorflow/core:all_kernels",
        "//tensorflow/core:core_cpu",
        "//tensorflow/core:framework",
        "//tensorflow/core:lib_internal",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
        "//tensorflow/core:testlib",
        "//tensorflow/core/kernels:ops_util",
    ],
)

filegroup(
    name = "all_files",
    srcs = glob(
        ["**/*"],
        exclude = [
            "**/METADATA",
            "**/OWNERS",
        ],
    ),
)
