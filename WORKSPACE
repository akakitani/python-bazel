workspace(name = "python_bazel")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")

# rules_foreign_cc is used to build Python interpreter from source
http_archive(
    name = "rules_foreign_cc",
    strip_prefix = "rules_foreign_cc-master",
    url = "https://github.com/bazelbuild/rules_foreign_cc/archive/master.zip",
)

load("@rules_foreign_cc//:workspace_definitions.bzl", "rules_foreign_cc_dependencies")
rules_foreign_cc_dependencies()

# See //third_party/python3
http_archive(
    name = "python_interpreter_src",
    urls = ["https://www.python.org/ftp/python/3.7.8/Python-3.7.8.tar.xz"],
    sha256 = "43a543404b363f0037f89df8478f19db2dbc0d6f3ffee310bc2997fa71854a63",
    strip_prefix = "Python-3.7.8",
    build_file_content = """
filegroup(
    name = "files",
    srcs = glob(["**"]),
    visibility = ["//visibility:public"],
)
""",
)

# openssl is required as a dependency for Python interpreter
all_content = """filegroup(name = "all", srcs = glob(["**"]), visibility = ["//visibility:public"])"""
http_archive(
    name = "openssl",
    build_file_content = all_content,
    strip_prefix = "openssl-OpenSSL_1_1_1d",
    urls = ["https://github.com/openssl/openssl/archive/OpenSSL_1_1_1d.tar.gz"]
)

# TODO: Use a real release...
git_repository(
    name = "rules_python",
    remote = "https://github.com/akakitani/rules_python.git",
    commit = "97efac825d280293272572039ada9f1fe2d203be",
)

load("@rules_python//python:repositories.bzl", "py_repositories")
py_repositories()
