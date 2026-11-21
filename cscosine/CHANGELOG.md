# Changelog of the cscosine fork of OpenCV

## v5.1.0-cpu.1 (and v5.1.0-cuda.1, to tag once csopencvcuda has built it)

- Rebased on upstream `5.1.0`. KleidiCV 26.09 dropped: upstream has it (opencv/opencv#30128).
- Branches renamed to the final layout: `main` (common), `cpu`, `cuda`; opencv_contrib follows the same layout and
  tags.

## v5.0.0-cpu.1

- One common stack on upstream `5.0.0` and one setup commit per variant.
- CPU: the same build as `v5.0.2-cpu.2` (built and released by csopencvcpu `v5.0.1-rc5`), tagged on the new layout.

## Before (history)

`v5.0.1-cpu`, `v5.0.1-cuda`, `v5.0.2-cpu`, `v5.0.2-cpu.1`, `v5.0.2-cpu.2`, `v5.0.2-cuda`: two separate branches on
upstream 5.0.0.
