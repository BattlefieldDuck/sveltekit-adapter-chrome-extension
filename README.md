# sveltekit-adapter-chrome-extension

[Adapter](https://kit.svelte.dev/docs#adapters) for SvelteKit apps that prerenders your site as a collection of static files and removes inline scripts to comply with content source policies of Chrome extensions using manifest v3.

> Based on [@sveltekit/adapter-static](https://github.com/sveltejs/kit/blob/master/packages/adapter-static). Credit goes to [these people](https://github.com/sveltejs/kit/graphs/contributors) for their hard work to make Svelte so great

> 🚧 If you are using SvelteKit v1.0.0+, make sure to set your `prerender=true` for every page reference by your extension so SvelteKit generates the HTML files.

## Usage

Install with `npm i -D sveltekit-adapter-chrome-extension`, then add the adapter to your `svelte.config.js`:

```js
// svelte.config.js
import adapter from "sveltekit-adapter-chrome-extension";

export default {
  kit: {
    adapter: adapter({
      // default options are shown
      pages: "build",
      assets: "build",
      fallback: null,
      precompress: false,
      manifest: "manifest.json",
      emptyOutDir: true,
    }),
    appDir: "app",
  },
};
```

## Options

### pages

The directory to write prerendered pages to. It defaults to `build`.

### assets

The directory to write static assets (the contents of `static`, plus client-side JS and CSS generated by SvelteKit) to. Ordinarily this should be the same as `pages`, and it will default to whatever the value of `pages` is, but in rare circumstances you might need to output pages and assets to separate locations.

### fallback

Specify a fallback page for SPA mode, e.g. `index.html` or `200.html` or `404.html`.

### precompress

If `true`, precompresses files with brotli and gzip. This will generate `.br` and `.gz` files.

### manifest

Specify manifest file name if you want different manifests for different target platforms, e.g. `chrome_manifest.json`, `firefox_manifest.json`.
This file name must match one that is present in the `static` directory (the dir containing your static files). The selected target file will be renamed to `manifest.json` in the build directory, and all other `.json` files with `manifest` in the name won't be copied.


### emptyOutDir

Specify if the output directory should automatically be emptied when building the project. Defaults to `true`.
Turn to `false` if you use alternate watch commands for which emptying the output directory may create conflicts. 

## License

[MIT](LICENSE)
