"""Targets in the repository root"""

load("@aspect_rules_js//js:defs.bzl", "js_library")
load("@gazelle//:def.bzl", "gazelle")
load("@npm//:defs.bzl", "npm_link_all_packages")

# TODO: remove once https://github.com/aspect-build/aspect-cli/issues/560 done
# gazelle:js_npm_package_target_name pkg
npm_link_all_packages(name = "node_modules")

js_library(
    name = "eslintrc",
    srcs = ["eslint.config.mjs"],
    visibility = ["//:__subpackages__"],
    deps = [
        ":node_modules/@eslint/js",
        ":node_modules/typescript-eslint",
    ],
)

js_library(
    name = "prettierrc",
    srcs = ["prettier.config.cjs"],
    visibility = ["//tools/format:__pkg__"],
    deps = [],
)

exports_files(
    [
    ],
    visibility = ["//:__subpackages__"],
)

# It's faster to avoid type-checking in a devserver when using monorepo packages.
# If you commonly ship your npm packages outside the repo, change this to "npm_package"
# gazelle:js_package_rule_kind js_library

# We prefer BUILD instead of BUILD.bazel
# gazelle:build_file_name BUILD
# gazelle:exclude githooks/*

gazelle(
    name = "gazelle",
    env = {
        "ENABLE_LANGUAGES": ",".join([
            "starlark",
            "js",
        ]),
    },
    gazelle = "@multitool//tools/gazelle",
)
