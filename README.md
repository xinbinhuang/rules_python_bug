# Reproducible example bug for https://github.com/bazelbuild/rules_python/issues/958

## Issue

`entry_point` rule no longer working when used with blzmod. 

### Using bzlmod

This repo default use `blzmod`. See `common --enable_bzlmod` in `.bazelrc`

It'll return error when run with the `flake8` in this repo

```bazel
❯ bazel build //:flake8
ERROR: /Users/xxx/projects/rules_python_bug/BUILD.bazel:3:6: no such package '@[unknown repo 'pip_flake8' requested from @]//': The repository '@[unknown repo 'pip_flake8' requested from @]' could not be resolved: No repository visible as '@pip_flake8' from main repository and referenced by '//:flake8'
ERROR: Analysis of target '//:flake8' failed; build aborted: Analysis failed
INFO: Elapsed time: 5.307s
INFO: 0 processes.
FAILED: Build did NOT complete successfully (1 packages loaded, 0 targets configured)
```

### Using `WORKSPACE`

Comment out `common --enable_bzlmod` in `.bazelrc`, and then rerun the bazel target again will succeed.

```bazel
❯ bazel build //:flake8
INFO: Analyzed target //:flake8 (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
Target @pip_flake8//:rules_python_wheel_entry_point_flake8 up-to-date:
  bazel-bin/external/pip_flake8/rules_python_wheel_entry_point_flake8
INFO: Elapsed time: 0.071s, Critical Path: 0.00s
INFO: 1 process: 1 internal.
INFO: Build completed successfully, 1 total action
```