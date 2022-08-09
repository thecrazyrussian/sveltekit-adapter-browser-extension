# sveltekit-adapter-browser-ext

[Adapter](https://kit.svelte.dev/docs#adapters) for SvelteKit which turns your app into a cross-platform browser extension.

## Provenance
Forked from [https://github.com/antony/sveltekit-adapter-browser-extension](https://github.com/antony/sveltekit-adapter-browser-extension) due to needng things working.
## Usage

Install with `npm i -D thecrazyrussian/sveltekit-adapter-browser-extension@0.4.0`, then add the adapter to your `svelte.config.js`.

Some additional configuration is required for this adapter to work - you need to (1) set ``appDir`` to something without an underscore and (2) tell kit to prerender its pages by default:

```js
// svelte.config.js
import adapter from 'thecrazyrusina/sveltekit-adapter-browser-extension';

export default {
	kit: {
		adapter: adapter({
			// default options are shown
			pages: 'build', // the output directory for the pages of your extension
			assets: undefined, // the asset output directory is derived from pages if not specified explicitly
			fallback: undefined, // set to true to output an SPA-like extension
			manifestVersion: 3, // the version of the automatically generated manifest (Version 3 is required by Chrome).
            manifest: {
                // You can customize manifest here
            }
        }),
		appDir: 'ext', // This is important - chrome extensions can't handle the default _app directory name.
		prerender: {
			default: true
		}
	}
};
```

## Try it

An example barebone app exists at `./example-app`. You can `npm run build` here and install the extension.

### To try with your own app:

Install the adapter and `npm run build`. Go to your browser's extension page and install unpacked extension - point it at the build directory within your app.

If you get an error about `_app` being a disallowed folder, delete `_app` from within the build dir. It appears there sometimes and I'm not sure why - I'll fix as soon as possible!

## Configuration

To specify your own manifest information (it will be merged with the generated one), simply have a manifest file local within your app directory. It grabs the package.json's version and name by default. Uses uppercased an split name for manifest deault action title.

## Roadmap

I am looking for help to build and maintain this module. Roadmap is:

* Specifying the type of extension via config
* Allowing icons and such to be driven by configuration

## License

[MIT](LICENSE)
