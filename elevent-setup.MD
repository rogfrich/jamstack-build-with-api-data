# Eleventy Setup

This is based on Phil Hawskworth's third example from [this video](https://www.netlify.com/blog/2020/03/12/learn-jamstack-with-a-free-3.5-hour-video-of-demos-and-examples/) where is is moving from a static site with just `index.html` and `vibe.js` to an eleventy one.

## Steps taken:
- `npm init --y` Creates a new npm package with the default setup.
- `npm i --save @11ty/eleventy` Installs eleventy.
- Modify the author in `package.json` if you want.
- Create the eleventy config file `.eleventy.js`
- Create a `src` folder for holding the source code, with a subdirectory `js` for any javascript.
- Create folder `src/_includes`
- Set up `base.njk` as the main template (in /_includes). Add a header with a link to the About Page...
- Set up `index.njk` as the first page content (using `base.njk` as the layout)
- Copy the `index.njk` to `about.njk` to be an about page.

So, now there are two pages under `src` which both use the base layout.

- Modify `.elevent.js` (which was empty) to have the following:

```
module.exports = function(config) {

    config.addPassthroughCopy("src/js");
    return {
        dir: {
            input: "src",
            output: "dist"
        }
    };

};
```

**N.B.** the pass through in the config file for javascript stuff so that anything in the `src/js` folder just gets passed across into the `dist` folder.

- Modify `package.json` replace the "test" script with a couple of others so it looks like:

```
  "scripts": {
    "build": "eleventy",
    "start": "eleventy --serve"
  },
```

You should now be able to run `npm run build` to get your site generated into the `dist` folder. Note that it generates and `about` folder for us to hold the *about* `index.html`

And you can also now run `npm start` to get eleventy to serve pages.

## Deploying
The manual approach would be to run the build and the copy the stuff out of the _dist folder over to a hosting environment, but it is better to set it up to deploy automatically.

- Add `.gitignore` and populate it thusly:
```
node_modules
dist
```
As we don't want to deploy our site as it will be rebuilt. Similarly the node stuff will be rebuilt on the hosting site.

- Initialise the Repo: `git init`
- Add our files: `git add .`
- Commit them: `git commit -m "Initial Version"`

