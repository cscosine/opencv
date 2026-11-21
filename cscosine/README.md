# opencv: the cscosine fork

OpenCV, as built and released by [csopencvcpu](https://github.com/cscosine/csopencvcpu) (CPU) and
[csopencvcuda](https://github.com/cscosine/csopencvcuda) (CUDA): the upstream release plus a few commits of ours, in
two variants. This folder is ours; the rest of the repository is upstream.

[opencv_contrib](https://github.com/cscosine/opencv_contrib) is built together with it and follows the same layout:
the same upstream release, the same branches, the same tags.

| | |
|---|---|
| Upstream | <https://github.com/opencv/opencv> (remote `upstream`; its tags are fetched, its branches are not copied) |
| Base | upstream tag `5.1.0` |
| License | upstream's (`LICENSE`, Apache-2.0) |

## Branches: one common stack, two variants

```
5.1.0 ── common commits ── main
                            ├── CPU setup  ── cpu    (csopencvcpu)    tags v<opencv>-cpu.<n>
                            └── CUDA setup ── cuda   (csopencvcuda)   tags v<opencv>-cuda.<n>
```

- `main`: what both variants need (`git log 5.1.0..main`).
- `cpu`, `cuda`: `main` plus one commit, the `csCMakeProjectSetup.json` of the variant (CUDA off / on, the CUDA
  architectures and locations). A change for both goes on `main`, then the variants are rebased on it.
- In opencv_contrib, `cpu` and `cuda` have no commit of their own (the variant is chosen by opencv's setup): they
  are the same as its `main`, and exist so that both forks are tagged the same way.

## Versions (an exception to the `-cs.N` of the other forks)

Tags `v<opencv version>-cpu.<n>` and `v<opencv version>-cuda.<n>`: the OpenCV version, the variant, our patch level
(e.g. `v5.1.0-cpu.1`), set on the variant's branch, with the same name in opencv and opencv_contrib. The
distributions keep the OpenCV version as theirs; their release tags follow the fork tag they ship
(`v5.1.0-cpu.1-rc1`, `v5.1.0-cpu.1`).

Older tags stay, because released builds point to them: `v5.0.0-cpu.1` (the 5.0.0 layout), `v5.0.0-cpu`,
`v5.0.0-cuda`, `v5.0.0-original`, `v5.0.1-*`, `v5.0.2-*` and `legacy-main-*` (the branches before this layout).

## Common changes

| Commit | Why |
|---|---|
| csCMake presets (`CMakePresets.json`) | Built with the csCMake presets on every platform |
| Windows: MSVC and clang-cl (libwebp AVX2 flag, MLAS) | clang-cl needs `-mavx2`; MLAS's GNU-syntax assembler is not supported by MSVC drivers; `<cstring>` (opencv/opencv#29885) |
| macOS: install RPATH `@loader_path`, contrib freetype off | The installed libraries find each other; no dependency on Homebrew's freetype / harfbuzz |

## Syncing with a new upstream release

Do it for opencv and opencv_contrib together. In each: fetch the new upstream tag, rebase `main` on it
(`git rebase --onto <new> <old> main`), drop what upstream has absorbed, rebase `cpu` and `cuda` on the new `main`,
force-push the three branches (the old heads stay reachable through their tags). Build through csopencvcpu /
csopencvcuda pointing at the new tags, then tag `v<new>-cpu.1` / `v<new>-cuda.1` in both forks.
