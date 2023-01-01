# This file marks the root of the Bazel workspace.
# See MODULE.bazel for dependencies and setup.
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "rules_python",
    sha256 = "497ca47374f48c8b067d786b512ac10a276211810f4a580178ee9b9ad139323a",
    strip_prefix = "rules_python-0.16.1",
    url = "https://github.com/bazelbuild/rules_python/archive/refs/tags/0.16.1.tar.gz",
)

load("@rules_python//python:pip.bzl", "pip_parse")

# Create a central repo that knows about the dependencies needed from
# requirements_lock.txt.
pip_parse(
   name = "pip",
   requirements_lock = "//py:requirements-lock.txt",
)
# Load the starlark macro which will define your dependencies.
load("@pip//:requirements.bzl", "install_deps")
# Call it to define repos for your requirements.
install_deps()