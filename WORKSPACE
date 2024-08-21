workspace(name = "com_github_brpc_braft")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "bazel_skylib",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.2.1/bazel-skylib-1.2.1.tar.gz",
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.2.1/bazel-skylib-1.2.1.tar.gz",
    ],
)

http_archive(
    name = "com_google_googletest",  # 2021-07-09T13:28:13Z
    sha256 = "12ef65654dc01ab40f6f33f9d02c04f2097d2cd9fbe48dc6001b29543583b0ad",
    strip_prefix = "googletest-8d51ffdfab10b3fba636ae69bc03da4b54f8c235",
    urls = ["https://github.com/google/googletest/archive/8d51ffdfab10b3fba636ae69bc03da4b54f8c235.zip"],
)

bind(
    name = "gtest",
    actual = "@com_google_googletest//:gtest",
)

http_archive(
    name = "com_google_protobuf",
    build_file = "//bazel/third_party:protobuf.BUILD",
    # sha256 = "87407cd28e7a9c95d9f61a098a53cf031109d451a7763e7dd1253abf8b4df422",
    patch_cmds = [
        "sed -i protobuf.bzl -re '4,4d;493,594d'",
    ],
    patch_cmds_win = [
        """$content = Get-Content 'protobuf.bzl' | Where-Object {
    -not ($_.ReadCount -ne 4) -and
    -not ($_.ReadCount -ge 418 -and $_.ReadCount -le 509)
}
Set-Content protobuf.bzl -Value $content -Encoding UTF8
""",
    ],
    strip_prefix = "protobuf-21.12",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/refs/tags/v21.12.tar.gz"],
)

http_archive(
    name = "com_github_gflags_gflags",  # 2018-11-11T21:30:10Z
    sha256 = "34af2f15cf7367513b352bdcd2493ab14ce43692d2dcd9dfc499492966c64dcf",
    strip_prefix = "gflags-2.2.2",
    urls = ["https://github.com/gflags/gflags/archive/v2.2.2.tar.gz"],
)

bind(
    name = "gflags",
    actual = "@com_github_gflags_gflags//:gflags",
)

http_archive(
    name = "com_github_google_glog",  # 2021-05-07T23:06:39Z
    patch_args = ["-p1"],
    patches = [
        "//bazel/third_party:0001-mark-override-resolve-warning.patch",
    ],
    sha256 = "21bc744fb7f2fa701ee8db339ded7dce4f975d0d55837a97be7d46e8382dea5a",
    strip_prefix = "glog-0.5.0",
    urls = ["https://github.com/google/glog/archive/v0.5.0.zip"],
)

bind(
    name = "glog",
    actual = "@com_github_google_glog//:glog",
)

http_archive(
    name = "com_github_google_leveldb",  # 2021-02-23T21:51:12Z
    build_file = "//bazel/third_party/leveldb:leveldb.BUILD",
    sha256 = "9a37f8a6174f09bd622bc723b55881dc541cd50747cbd08831c2a82d620f6d76",
    strip_prefix = "leveldb-1.23",
    urls = [
        "https://github.com/google/leveldb/archive/refs/tags/1.23.tar.gz",
    ],
)

http_archive(
    name = "com_github_google_crc32c",  # 2021-10-05T19:47:30Z
    build_file = "//bazel/third_party:crc32c.BUILD",
    patch_tool = "patch",
    patch_args = ["-p1"],
    patches = ["//bazel:configure_template.bzl.patch"],
    sha256 = "ac07840513072b7fcebda6e821068aa04889018f24e10e46181068fb214d7e56",
    strip_prefix = "crc32c-1.1.2",
    urls = ["https://github.com/google/crc32c/archive/1.1.2.tar.gz"],
)

http_archive(
    name = "com_github_google_snappy",
    build_file = "//bazel/third_party:snappy.BUILD",
    sha256 = "7ee7540b23ae04df961af24309a55484e7016106e979f83323536a1322cedf1b",
    strip_prefix = "snappy-1.2.0",
    urls = [
        "https://github.com/google/snappy/archive/1.2.0.zip",
    ],
)

http_archive(
    name = "openssl",  # 2021-12-14T15:45:01Z
    build_file = "//bazel/third_party:openssl.BUILD",
    sha256 = "f89199be8b23ca45fc7cb9f1d8d3ee67312318286ad030f5316aca6462db6c96",
    strip_prefix = "openssl-1.1.1m",
    urls = [
        "https://www.openssl.org/source/openssl-1.1.1m.tar.gz",
        "https://github.com/openssl/openssl/archive/OpenSSL_1_1_1m.tar.gz",
    ],
)

http_archive(
    name = "com_github_madler_zlib",
    build_file = "//bazel/third_party:zlib.BUILD",
    # sha256 = "1525952a0a567581792613a9723333d7f8cc20b87a81f920fb8bc7e3f2251428",
    strip_prefix = "zlib-1.3.1",
    urls = [
        "https://github.com/madler/zlib/archive/refs/tags/v1.3.1.tar.gz",
    ],
)

#http_archive(
#    name = "com_github_brpc_brpc",
#    strip_prefix = "incubator-brpc-2b748f82c3447196c8ce372733e5af8f8d76cef5",
#    url = "https://github.com/apache/incubator-brpc/archive/2b748f82c3447196c8ce372733e5af8f8d76cef5.tar.gz",
#)

http_archive(
    name = "rules_foreign_cc",
    sha256 = "4b33d62cf109bcccf286b30ed7121129cc34cf4f4ed9d8a11f38d9108f40ba74",
    strip_prefix = "rules_foreign_cc-0.11.1",
    url = "https://github.com/bazelbuild/rules_foreign_cc/releases/download/0.11.1/rules_foreign_cc-0.11.1.tar.gz",
)

load("@rules_foreign_cc//foreign_cc:repositories.bzl", "rules_foreign_cc_dependencies")
rules_foreign_cc_dependencies(register_preinstalled_tools = True)

http_archive(
    name = "rules_perl",
    sha256 = "3e52a9ab4162d59318adddb911794ff884c30477fb1dcdad92f8fb533edf9110",
    strip_prefix = "rules_perl-0.2.0",
    urls = [
        "https://github.com/bazelbuild/rules_perl/archive/refs/tags/0.2.0.tar.gz",
    ],
)

load("@rules_perl//perl:deps.bzl", "perl_register_toolchains")
perl_register_toolchains()

local_repository(
    name = "com_github_brpc_brpc",
    path = "../brpc",
)

bind(
    name = "brpc",
    actual = "@com_github_brpc_brpc//:brpc",
)

bind(
    name = "butil",
    actual = "@com_github_brpc_brpc//:butil",
)