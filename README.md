# Reproduction repo for potential webpack bug

In some cases, Webpack is generating invalid source maps which cannot be consumed by node in `--enable-source-maps` mode. I've observed that when the project contains for example an [ajv](https://www.npmjs.com/package/ajv) or [mongodb](https://www.npmjs.com/package/mongodb) dependency the nodejs is not able to map stack trace using source maps.

I believe this is a webpack issue because, when I bundle the same project with for example esbuild the node is working well with generated source maps. 

## To verify
Repo already contains output bundle but feel free to generate it on your own running `yarn build` in each project.

- Run `yarn start` in `working` project and see that stack trace was mapped properly.
- Run `yarn start` in `not_working` project and see that stack trace points to bundle file (dist/index.js)
- Build same with esbuild by `yarn build2` and run `yarn start` to see that source map from esbuild is properly interpreted by node.