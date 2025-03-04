load(
    "//bazel:envoy_build_system.bzl",
    "envoy_package",
)
load(
    "//test/extensions:extensions_build_system.bzl",
    "envoy_extension_cc_test",
)

licenses(["notice"])  # Apache 2

envoy_package()

envoy_extension_cc_test(
    name = "datadog_tracer_impl_test",
    srcs = [
        "agent_http_client_test.cc",
        "datadog_tracer_impl_test.cc",
        "dict_util_test.cc",
        "logger_test.cc",
        "span_test.cc",
        "time_util_test.cc",
        "tracer_stats_test.cc",
    ],
    copts = [
        # Make sure that headers included from dd_trace_cpp use Abseil
        # equivalents of std::string_view and std::optional.
        "-DDD_USE_ABSEIL_FOR_ENVOY",
    ],
    extension_names = ["envoy.tracers.datadog"],
    external_deps = [
        "dd_trace_cpp",
    ],
    # TODO(wrowe): envoy_extension_ rules don't currently exclude windows extensions
    tags = ["skip_on_windows"],
    deps = [
        "//source/common/common:base64_lib",
        "//source/common/http:header_map_lib",
        "//source/common/http:headers_lib",
        "//source/common/http:message_lib",
        "//source/common/runtime:runtime_lib",
        "//source/extensions/tracers/datadog:datadog_tracer_lib",
        "//test/mocks/http:http_mocks",
        "//test/mocks/local_info:local_info_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/stats:stats_mocks",
        "//test/mocks/thread_local:thread_local_mocks",
        "//test/mocks/tracing:tracing_mocks",
        "//test/mocks/upstream:cluster_manager_mocks",
        "//test/mocks/upstream:thread_local_cluster_mocks",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/trace/v3:pkg_cc_proto",
    ],
)

envoy_extension_cc_test(
    name = "config_test",
    srcs = ["config_test.cc"],
    extension_names = ["envoy.tracers.datadog"],
    # TODO(wrowe): envoy_extension_ rules don't currently exclude windows extensions
    tags = ["skip_on_windows"],
    deps = [
        "//source/extensions/tracers/datadog:config",
        "//test/mocks/server:server_mocks",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/trace/v3:pkg_cc_proto",
    ],
)
