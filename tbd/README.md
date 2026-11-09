# Optional modern TBD overlay (proposal)

Canonical files outside this directory retain their original upstream content,
including intentionally v1 TBD files used by older toolchains. Do not add this
path to the default search paths for those toolchains.

`modern/` is an alternate linker-only tree requiring both TBD v3 and v4 support.
It contains explicitly tagged versions of legacy stubs, plus the existing modern
stubs. It contains no headers or modules and must be used only for linking. Cycript uses v4 with explicit device/simulator
targets; it is not a v3-compatible stub. The two libsubstrate aliases are
materialized as stubs so Windows clones without symlink support can link them.

Consumers must retain the canonical paths for compilation and headers, and for
libraries not present in the overlay (such as libroot.a). For rootless linking,
use `modern/iphone/rootless`, not the rootful overlay. Prefer this tree only for
a selected linker proven to support both formats. The current consumer proposal
limits automatic selection to the native Windows clang/LLD path; it is not a
universal libtapi capability-selection solution.

This layout is a proposal pending maintainer agreement. Legacy linker execution
and all Cycript architecture/platform combinations have not been tested. The
preservation of canonical file content is mechanically checked against upstream,
but that alone is not a claim that every legacy toolchain has been tested.
