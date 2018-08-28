# rules_go_ios_arm
Sample rules_go project that fails to build with ios_arm/go 1.11

Issue is at https://github.com/bazelbuild/rules_go/issues/1693.

Works with Go 1.10 or `--config ios_arm64`, but fails with Go 1.11 + `--config ios_arm`.

Run with
```
bazel build --config ios_arm //:cmd
```

Should fail with:
```
ERROR: /Users/steeve/go/src/github.com/steeve/rules_go_ios_arm/BUILD.bazel:3:1: GoLink darwin_arm/cmd failed (Exit 1): link failed: error executing command
  (cd /private/var/tmp/_bazel_steeve/9cd886b034874139736cde03e330905f/execroot/__main__ && \
  exec env - \
    APPLE_SDK_PLATFORM=iPhoneOS \
    APPLE_SDK_VERSION_OVERRIDE=11.4 \
    CGO_ENABLED=1 \
    GOARCH=arm \
    GOOS=darwin \
    GOROOT=bazel-out/ios_armv7-fastbuild/bin/external/io_bazel_rules_go/darwin_arm/stdlib% \
    GOROOT_FINAL=GOROOT \
    PATH=/usr/bin \
  bazel-out/host/bin/external/io_bazel_rules_go/go/tools/builders/darwin_amd64_stripped/link -sdk external/go_sdk -installsuffix darwin_arm -tags ios -package_list bazel-out/host/bin/external/go_sdk/packages.txt -o bazel-out/ios_armv7-fastbuild/bin/darwin_arm/cmd -main bazel-out/ios_armv7-fastbuild/bin/darwin_arm/cmd%/cmd.a -- -extld external/local_config_cc/cc_wrapper.sh -extldflags '-headerpad_max_install_names -lc++ -no-canonical-prefixes -target armv7-apple-ios -miphoneos-version-min=7.0')

Use --sandbox_debug to see verbose messages from the sandbox
sync.(*Map).Load: relocation target sync/atomic.(*Value).Load not defined
sync.(*Map).Store: relocation target sync/atomic.(*Value).Load not defined
sync.(*Map).LoadOrStore: relocation target sync/atomic.(*Value).Load not defined
sync.(*Map).dirtyLocked: relocation target sync/atomic.(*Value).Load not defined
internal/testlog.Logger: relocation target sync/atomic.(*Value).Load not defined
GoLink: error running subcommand: exit status 2
Target //:cmd failed to build
INFO: Elapsed time: 76.168s, Critical Path: 49.95s
INFO: 10 processes: 10 darwin-sandbox.
FAILED: Build did NOT complete successfully
```

