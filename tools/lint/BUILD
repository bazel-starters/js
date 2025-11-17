"""Definition of linter tools

This is in its own package because it has so many loading-time symbols,
we don't want to trigger eager fetches of these for builds which aren't running linters.
"""

load("@npm//:eslint/package_json.bzl", eslint_bin = "bin")

package(default_visibility = ["//:__subpackages__"])

eslint_bin.eslint_binary(name = "eslint")
