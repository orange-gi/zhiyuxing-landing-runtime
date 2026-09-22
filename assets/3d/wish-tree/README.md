# Wish tree · Landing Web runtime

This directory contains the web-runtime derivative of the wish-tree Blender master. It is **not** a second art source.

## Source of truth

- Repository: `orange-gi/agent-zhiyuxing-product`
- Asset: `materials/brand-objects/wish-tree/natural-refinement/wish-tree-natural.glb`
- Stage: `natural-refinement-r03` (2026-09-22)
- Source GLB SHA-256: `1ede1492d8c34f61464276b1f93b4a40929b20f9a9723bb2aaa7a78256738995`
- Source: 69,327,664 bytes, 1,727,948 triangles, 38 meshes
- Root: `ZYX_WISH_TREE`
- Stable anchors: `ANCHOR_before`, `ANCHOR_begin`, `ANCHOR_now`

Do not hand-edit the web GLB. Art changes start in the Blender/master asset and then regenerate this derivative.

## Web derivative

`wish-tree-natural-r03-web.glb`

- SHA-256: `c49d91f192031ed1b6727fb88acf832d852430a13666aceaffac87966848293c`
- Size: 6,017,932 bytes
- Upload vertices: 471,082
- Render vertex count reported by glTF Transform: 1,448,994
- Bounds and all three named anchors are preserved
- Required extensions: `EXT_meshopt_compression`, `EXT_texture_webp`, `KHR_mesh_quantization`
- Three.js runtime: existing project `three@0.185.1`; no React Three Fiber or CDN decoder was added

Generated with glTF Transform 4.5.0:

```bash
pnpm dlx @gltf-transform/cli optimize \
  wish-tree-natural.glb wish-tree-natural-r03-web.glb \
  --compress meshopt \
  --flatten false \
  --join false \
  --instance false \
  --palette false \
  --prune false \
  --simplify true \
  --simplify-ratio 0.28 \
  --simplify-error 0.0015 \
  --simplify-lock-border false \
  --texture-compress webp \
  --texture-size 1024
```

The earlier 10.57 MB border-locked candidate did not reduce the disconnected leaf geometry enough. An 8.67 MB / ratio 0.45 candidate also passed loading, but the 6.02 MB derivative is the selected Landing LOD.

## Poster and progressive loading

`wish-tree-natural-r03-poster.webp`

- Source: the actual r03 Blender front render
- SHA-256: `5d4b40d669f8e8b72d0e127df07855753287b55ece4de75e99ef5113c8ade408`
- Size: 171,046 bytes
- 1440×1080 WebP

The `/wish-tree` page renders the poster immediately. The Three.js scene is code-split and enabled after the first paint. The GLB then replaces the poster without a loading screen. The homepage must not load this scene or request the GLB.

Poster-only fallback is intentional for Save-Data, 2G-class connections, <=2 GB reported device memory, WebGL creation/load failures, and detected software renderers such as SwiftShader/llvmpipe. `?three-review=1` is an internal forced-3D QA path and uses a reduced frame rate on software rendering.

## Interaction

The `/wish-tree` page uses the same existing procedural wish-plaque implementation as the product wish-tree experience. The homepage only links into this page and does not render the 3D tree.

1. Plaque remains attached to `ANCHOR_now`.
2. First click moves the camera toward the original branch/anchor.
3. Second click flips the plaque in place.
4. Third click returns to the full tree.

The tree is not turned into a floating 3D UI card.

## QA

Run:

```bash
npm run build
CHROMIUM_BIN=/data/runtimes/chromium/153.0.8010.0-linux-x64/chromium \
  node scripts/qa-wish-tree-landing.mjs
```

2026-09-22 browser QA passed:

- desktop 1440×1000: model loaded, plaque focus + flip passed
- mobile 390×844: model loaded, plaque focus + flip passed
- console errors: 0
- failed requests: 0
- Save-Data fallback: poster only
- SwiftShader/software-renderer fallback: poster only
- homepage boundary: 0 3D scene instances and 0 GLB requests
- server-side static capture sanity: 723×542, non-blank/high-variance render evidence

The r03 Blender art candidate keeps its own art-approval lifecycle. This Landing derivative does not redefine or supersede that visual approval.
