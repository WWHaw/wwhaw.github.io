# Termux Astro project creation

## 1. Empty and Basic template
```
pnpm create astro@latest
cd project_directory
~/astro/compiler-rs/install-android-binding.sh
pnpm run dev
```

## 2. Docs template
```
pnpm create astro@latest
cd project_directory
pnpm add @bruits/satteri-wasm32-wasi@0.10.5
pnpm add @bruits/satteri-wasm32-wasi@0.9.5
find node_modules/.pnpm \
  -path '*/@bruits/satteri-wasm32-wasi/satteri_napi.wasi.cjs' \
  -exec sed -i \
  's/const __rootDir = __nodePath.parse(process.cwd()).root/const __rootDir = process.cwd()/' {} \;
sed -i 's/: "astro/: "NAPI_RS_FORCE_WASI=true astro/g' package.json
sed -i "s#export default defineConfig({#export default defineConfig({\nimage: {\n    service: {\n        entrypoint: 'astro/assets/services/noop',\n    },\n},\n#g" astro.config.mjs
~/astro/compiler-rs/install-android-binding.sh
pnpm run dev
```

## 3. Blog template
```
pnpm create astro@latest
cd project_directory
pnpm add @astrojs/compiler-binding-wasm32-wasi@0.4.0
pnpm add @bruits/satteri-wasm32-wasi@0.10.5
find node_modules/.pnpm \
  -path '*/@astrojs/compiler-binding-wasm32-wasi/astro.wasi.cjs' \
  -exec sed -i \
  's/const __rootDir = __nodePath.parse(process.cwd()).root/const __rootDir = process.cwd()/' {} \;
find node_modules/.pnpm \
  -path '*/@bruits/satteri-wasm32-wasi/satteri_napi.wasi.cjs' \
  -exec sed -i \
  's/const __rootDir = __nodePath.parse(process.cwd()).root/const __rootDir = process.cwd()/' {} \;
sed -i 's/: "astro/: "NAPI_RS_FORCE_WASI=true astro/g' package.json
sed -i "s#export default defineConfig({#export default defineConfig({\nimage: {\n    service: {\n        entrypoint: 'astro/assets/services/noop',\n    },\n},\n#g" astro.config.mjs
~/astro/compiler-rs/install-android-binding.sh
pnpm run dev
```

