# Description:
#   Tools for building the Nucleus pip package.

# KEEP THIS LINE to import nucleus.bzl externally

licenses(["notice"])  # Apache License 2.0

filegroup(
    name = "licenses",
    data = [
        "//third_party:abseil_cpp.LICENSE",
        "//third_party:bazel.LICENSE",
        "//third_party:clif.LICENSE",
        "//:LICENSE",
        "@htslib//:LICENSE",
        # The following dependencies contain LICENSE files, but
        # don't define proper BUILD files and/or don't export the LICENSE files.
        # TODO(thomaswc): Copy these LICENSES to third_party, or
        # write pull requests for exporting them.
        # "@com_google_absl_py//:LICENSE",
        # "@com_google_googletest//:LICENSE",
        # "@com_googlesource_code_cctz//:LICENSE.txt",
        # "@io_bazel_rules_closure//:LICENSE",
        "@org_tensorflow//:LICENSE",
        "@protobuf_archive//:LICENSE",
    ],
)

# This is a fake target, designed to populate build_pip_package.runfiles
# with the right dependency files (including the __init__.py's).  It is testonly
# so that it may depend on testonly targets in nucleus/testing.
py_binary(
    name = "setup",
    testonly = 1,
    srcs = ["setup.py"],
    legacy_create_init = 1,
    deps = [
        "//nucleus/examples:examples_py",
        "//nucleus/io:io_py",
        "//nucleus/testing:testing_py",
        "//nucleus/util:util_py",
        "//nucleus/vendor/python:statusor_examples",
    ],
)

PIP_DEPS = [
    ":setup",
    ":licenses",
    "setup.py",
    "//:all_extensions",
]

sh_binary(
    name = "build_pip_package",
    testonly = 1,
    srcs = ["build_pip_package.sh"],
    data = PIP_DEPS,
)
