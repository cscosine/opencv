# Changelog of the cscosine fork of OpenCV

## v5.0.0-cpu.1 (and v5.0.0-cuda.1, to tag once csopencvcuda has built it)

- One common stack on upstream `5.0.0` (`dev`) and one setup commit per variant (`dev-cpu`, `dev-cuda`).
- CPU: the same build as `v5.0.2-cpu.2` (built and released by csopencvcpu `v5.0.1-rc5`): tagged on the new layout. CUDA: gets the common fixes it lacked (Windows clang-cl, MLAS, macOS RPATH,
  KleidiCV 26.09), built when csopencvcuda is revived.

## Before (history)

`v5.0.1-cpu`, `v5.0.1-cuda`, `v5.0.2-cpu`, `v5.0.2-cpu.1`, `v5.0.2-cpu.2`, `v5.0.2-cuda`: two separate branches on
upstream 5.0.0.
