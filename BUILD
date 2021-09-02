load("@build_bazel_rules_nodejs//:index.bzl", "pkg_npm")
load("@npm//@bazel/typescript:index.bzl", "ts_project")

ts_project(
    srcs = glob(["src/**/*.ts"]),
    root_dir = "src",
    out_dir = "dist",
    source_map = True,
    declaration = True,
    declaration_map = True,
    incremental = True,
)

pkg_npm(
    name = "pkg_npm",
    package_name = "bazel-ts-maps",
    srcs = [
        "package.json",
    ] + glob(["src/**/*.ts"]),
    deps = ["tsconfig"],
)
