load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_rust",
    sha256 = "190b5aeba104210f8ed9b1ff595d1f459297fe32db70f0a04f5c537a13ee0602",
    urls = ["https://github.com/bazelbuild/rules_rust/releases/download/0.24.1/rules_rust-v0.24.1.tar.gz"],
)

load("@rules_rust//rust:repositories.bzl", "rules_rust_dependencies", "rust_register_toolchains")

rules_rust_dependencies()

rust_register_toolchains(
    edition = "2021",
)

load("@rules_rust//crate_universe:repositories.bzl", "crate_universe_dependencies")

crate_universe_dependencies(bootstrap = True)

load("@rules_rust//crate_universe:defs.bzl", "crates_repository")

crates_repository(
    name = "crate_index",
    cargo_lockfile = "//:Cargo.lock",
    # `generator` is not necessary in official releases.
    # See load satement for `cargo_bazel_bootstrap`.
    generator = "@cargo_bazel_bootstrap//:cargo-bazel",
    manifests = ["//:Cargo.toml"],
)

load(
    "@crate_index//:defs.bzl",
    cargo_local_crate_repositories = "crate_repositories",
)

cargo_local_crate_repositories()
