licenses(["notice"])  # Apache 2

cc_library(
    name = "envoy_jni_interface_lib",
    srcs = ["jni_interface.cc"],
    copts = ["-std=c++14"],
    linkopts = [
        "-lm",
        "-llog",
    ],
    deps = ["//library/common:envoy_main_interface_lib"],
)

# Work around for transtive dependencies related to not including cc_libraries for kt_jvm_library
# Related to: https://github.com/bazelbuild/rules_kotlin/issues/132
#
# This work around is to use an empty java_library to include the cc_library dependencies needed
# for the kotlin jni layer
android_library(
    name = "java_cc_alias",
    srcs = ["library/kotlin/io/envoyproxy/envoymobile/EnovyKotlinEmptyClass.java"],
    custom_package = "io.envoyproxy.envoymobile",
    manifest = "library/EnvoyManifest.xml",
    deps = ["envoy_jni_interface_lib"],
)

kt_android_library(
    name = "android_lib",
    srcs = ["library/kotlin/io/envoyproxy/envoymobile/Envoy.kt"],
    custom_package = "io.envoyproxy.envoymobile",
    manifest = "library/EnvoyManifest.xml",
    deps = ["java_cc_alias"],
)