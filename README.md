# gamma-inspector

A heavily, heavily WIP inspector tool for Gamma Driver. More of a PoC than a useful tool at this point.

## Overview

The low level goals (many initially cribbed from the [WebGL Inspector](https://github.com/benvanik/WebGL-Inspector):

 * Capture (individual, and burst) frame traces
   * Allow filtering of commands
   * Summarize statistic for a frame (draw call count, resources created, render time, etc.)
   * Replay frame draw or individual draw calls
 * Inspect all buffers, visualizing the data inside based off of the draw call last used for it.
 * Visualize textures that have been used in the lifetime of a GL context
 * Inspect program compilation and input
 * For all of the above resources, see how they were used/referenced within a frame

Future higher-level goals:

 * Visualize the state of the WebGL state-machine at a point in time, including what vertexAttribs were enabled, what buffers/textures were bound to them, and the state of the uniforms at draw-call time.
 * Allow several meshes that have been rendered (one or more times) to be combined together and serialized out to a glTF or transit filel
 * Create texture atlases from uploaded textures.
 * Visualize a scene in preview using (currently non-existent) semantic information from the program inputs.
 * Diff frames by their states for debugging.
 

## Setup

Very alpha right now, and will be better once the cljsjs version of Facebook Data Table is fixed (watch [this issue](https://github.com/cljsjs/packages/issues). In the project you wish to use Gamma Inspector,

```
mkdir yaks
cd yaks
git clone git@github.com:sgrove/gamma-inspector.git
```

Then in your `project.clj`, under the dev `:cljsbuild`, add `:source-paths ["yaks/gamma-inspector/src"]`. Under the `:compiler` options for that build, add in an addition `:foreign-libs` entry:

```clojure

:foreign-libs [{:file "yaks/gamma-inspector/resources/public/js/vendor/fixed-data-table/fixed-data-table.js"
                                                        :provides ["facebook.react.fixed-data-table"]}]

```

Finally, wget and include [the css](https://raw.githubusercontent.com/facebook/fixed-data-table/master/dist/fixed-data-table.css) in your site somewhere 

## License

Copyright © 2015 Sean Grove

Distributed under the Eclipse Public License either version 1.0 or (at your option) any later version.
