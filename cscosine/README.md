# opencv: the cscosine fork

OpenCV, as built and released by [csopencvcpu](https://github.com/cscosine/csopencvcpu) (CPU) and
[csopencvcuda](https://github.com/cscosine/csopencvcuda) (CUDA): the upstream release plus a few commits of ours, in
two variants. This folder is ours; the rest of the repository is upstream. (`opencv_contrib`: its own fork.)

| | |
|---|---|
| Upstream | <https://github.com/opencv/opencv> |
| Base | upstream tag `5.0.0` (also in this repository; `main-original` follows upstream) |
| License | upstream's (`LICENSE`, Apache-2.0) |

## Branches: one common stack, two variants

```
5.0.0 ── common fixes ── dev
                          ├── CPU setup  ── dev-cpu    (csopencvcpu)    tags v<opencv>-cpu.<n>
                          └── CUDA setup ── dev-cuda   (csopencvcuda)   tags v<opencv>-cuda.<n>
```

- `dev`: what both variants need (`git log 5.0.0..dev`).
- `dev-cpu`, `dev-cuda`: `dev` plus one commit, the `csCMakeProjectSetup.json` of the variant (CUDA off / on, the
  CUDA architectures and locations). A change for both goes on `dev`, then the variants are rebased on it.
- `main-cpu`, `main-cuda`: the last release of each variant.

## Versions (an exception to the `-cs.N` of the other forks)

Tags `v<opencv version>-cpu.<n>` and `v<opencv version>-cuda.<n>`: the OpenCV version, the variant, our patch level
(e.g. `v5.0.0-cpu.1`). The distributions keep the OpenCV version as theirs (`5.0.0`); their release tags follow the
fork tag they ship. Older tags (`v5.0.1-*`, `v5.0.2-*`) are the history before this layout.

## Common changes

| Commit | Why |
|---|---|
| csCMake presets (`CMakePresets.json`) | Built with the csCMake presets on every platform |
| Windows: MSVC and clang-cl (libwebp AVX2 flag, MLAS) | clang-cl needs `-mavx2`; MLAS's GNU-syntax assembler is not supported by MSVC drivers; `<cstring>` (opencv/opencv#29885) |
| macOS: install RPATH `@loader_path`, contrib freetype off | The installed libraries find each other; no dependency on Homebrew's freetype / harfbuzz |
| KleidiCV 26.09 | Builds with GCC >= 15 (as upstream OpenCV 5.x, PR #30128) |

## Syncing with a new upstream release

Fetch the new upstream tag, rebase `dev` on it (`git rebase --onto <new> 5.0.0 dev`), drop what upstream has absorbed,
rebase `dev-cpu` and `dev-cuda` on the new `dev`, build through csopencvcpu / csopencvcuda, then tag
`v<new>-cpu.1` / `v<new>-cuda.1`.
