# Changelog of the cscosine fork of OpenCV

## v5.1.0-cpu.2 (and v5.1.0-cuda.1, to tag once csopencvcuda has built it)

- MLAS: assemble with the build's C compiler. With CMake < 4, `check_language(ASM)` picked GCC's `cc` in a clang
  build, which failed on the clang-only `-Wcast-function-type-strict` (Linux clang jobs of `v5.1.0-cpu.1`).

## v5.1.0-cpu.1 (never released: the Linux clang builds failed)

- Rebased on upstream `5.1.0`. KleidiCV 26.09 dropped: upstream has it (opencv/opencv#30128).
- Branches renamed to the final layout: `main` (common), `cpu`, `cuda`; opencv_contrib follows the same layout and
  tags.

## v5.0.0-cpu.1

- One common stack on upstream `5.0.0` and one setup commit per variant.
- CPU: the same build as `v5.0.2-cpu.2` (built and released by csopencvcpu `v5.0.1-rc5`), tagged on the new layout.

## Before (history)

`v5.0.1-cpu`, `v5.0.1-cuda`, `v5.0.2-cpu`, `v5.0.2-cpu.1`, `v5.0.2-cpu.2`, `v5.0.2-cuda`: two separate branches on
upstream 5.0.0.
