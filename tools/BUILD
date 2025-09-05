"""
Build supporting tools.

The tools subpackage is used to define build rules and configurations for tools
used throughout the repository. Firstparty tools not required for build support
should live elsewhere.

Of special note is that we're using the `bazel_env.bzl` tool to re-export tools
used under Bazel as a `bin/` tree which can be added to the `$PATH`. The
included `.envrc` automates this for you.

"""

load("@bazel_env.bzl", "bazel_env")
load("@bazelrc-preset.bzl", "bazelrc_preset")
load("@multitool//:tools.bzl", MULTITOOL_TOOLS = "TOOLS")
load("@npm//:defs.bzl", "npm_link_all_packages")
load("@npm//tools:yo/package_json.bzl", yo_bin = "bin")

package(default_visibility = ["//visibility:public"])

bazelrc_preset(name = "preset")

npm_link_all_packages(name = "node_modules")

yo_bin.yo_binary(name = "yo")

bazel_env(
    name = "bazel_env",
    toolchains = {
        "nodejs": "@nodejs_toolchains//:resolved_toolchain",
    },
    tools = {
        # Mapping from tool binary name ($PATH entry) to Bazel label
        "buildifier": "@buildifier_prebuilt//:buildifier",
        "format": "//tools/format:format",
        "node": "$(NODE_PATH)",
        "pnpm": "@pnpm",
        "yo": ":yo",
    } | MULTITOOL_TOOLS,
)
