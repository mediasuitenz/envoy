load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_extension",
    "envoy_cc_library",
    "envoy_extension_package",
    "envoy_select_enable_http3",
)

licenses(["notice"])  # Apache 2

# L4 network filter that implements HTTP protocol handling and filtering. This filter internally
# drives all of the L7 HTTP filters.
# Public docs: https://envoyproxy.io/docs/envoy/latest/configuration/http/http_conn_man/http_conn_man

envoy_extension_package()

envoy_cc_extension(
    name = "config",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    # This is core Envoy config.
    visibility = ["//visibility:public"],
    deps = [
        ":dependency_manager",
        "//envoy/config:config_provider_manager_interface",
        "//envoy/filesystem:filesystem_interface",
        "//envoy/http:codec_interface",
        "//envoy/http:filter_interface",
        "//envoy/http:original_ip_detection_interface",
        "//envoy/http:request_id_extension_interface",
        "//envoy/registry",
        "//envoy/router:route_config_provider_manager_interface",
        "//envoy/server:admin_interface",
        "//envoy/server:options_interface",
        "//envoy/stats:stats_interface",
        "//source/common/access_log:access_log_lib",
        "//source/common/common:minimal_logger_lib",
        "//source/common/config:utility_lib",
        "//source/common/filter:config_discovery_lib",
        "//source/common/http:conn_manager_lib",
        "//source/common/http:default_server_string_lib",
        "//source/common/http:request_id_extension_lib",
        "//source/common/http:utility_lib",
        "//source/common/http/http1:codec_lib",
        "//source/common/http/http1:settings_lib",
        "//source/common/http/http2:codec_lib",
        "//source/common/http/http3:codec_stats_lib",
        "//source/common/json:json_loader_lib",
        "//source/common/local_reply:local_reply_lib",
        "//source/common/protobuf:utility_lib",
        "//source/common/router:rds_lib",
        "//source/common/router:scoped_rds_lib",
        "//source/common/runtime:runtime_lib",
        "//source/common/tracing:http_tracer_lib",
        "//source/common/tracing:http_tracer_manager_lib",
        "//source/common/tracing:tracer_config_lib",
        "//source/common/tracing:custom_tag_lib",
        "//source/extensions/filters/http/common:pass_through_filter_lib",
        "//source/extensions/filters/network:well_known_names",
        "//source/extensions/filters/network/common:factory_base_lib",
        "//source/extensions/http/original_ip_detection/xff:config",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/extensions/filters/network/http_connection_manager/v3:pkg_cc_proto",
        "@envoy_api//envoy/extensions/request_id/uuid/v3:pkg_cc_proto",
        "@envoy_api//envoy/extensions/http/original_ip_detection/xff/v3:pkg_cc_proto",
        "@envoy_api//envoy/type/tracing/v3:pkg_cc_proto",
        "@envoy_api//envoy/type/v3:pkg_cc_proto",
    ] + envoy_select_enable_http3([
        "//source/common/quic:codec_lib",
    ]),
)

envoy_cc_library(
    name = "dependency_manager",
    srcs = ["dependency_manager.cc"],
    hdrs = ["dependency_manager.h"],
    external_deps = [
        "abseil_status",
    ],
    deps = [
        "@envoy_api//envoy/extensions/filters/common/dependency/v3:pkg_cc_proto",
    ],
)
