# Adding Placeholder Images to Your Documents

## Overview

The `{{< placeholder >}}` shortcode generates a placeholder image, which is incredibly useful when you’re designing your document or website layout but the final images aren’t ready yet. It helps maintain the design integrity without interrupting the development flow. Placeholder images can have configurable sizes and will be generated in either PNG or SVG format.

## Example

Here’s an example of a placeholder image:

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGQAAABkCAYAAABw4pVUAAADNklEQVR4nO2WLVYrQRBGKwuADcAGYAGAwuFQ4MAEBwYcDgUKBwoHBhwoXFxUsoG4uGQBSRaQ13dyKpDAE5jJJ757zuT09E81p25XD41+vz8NI4OFiGEhYliIGBYihoWIYSFiWIgYFiKGhYhhIWJYiBgWIoaFiGEhYliIGBYihoWIYSFiWIgYFiKGhYhhIWJYiBgWIoaFiGEhYliIGBYihoWIYSFiWIgYFiKGhYhhIWJYiBgWIoaFiGEhYliIGBYihoWIsVIhvV4vtre3S+uLwWBQfiM2NzfL7xfdbjd2d3dL6+8Qc319vXoS+uC3fba2thbm1slKhJCMi4uLSkjZv/TMuL29jeFwWFoRBwcHcXx8XM29vr6uZJCsp6enPyXr9PQ0Op1OvL6+xt7eXumJeH9/j1arVVoRGxsbcXNzE+PxOM7Pz+f73N/f/5BVBysRkpycnMTb21tpRZUQ3j8/P8tbxP7+frTb7Xh4eKgSgxwSybyzs7MyY7bm4+Mjms1mwMvLSxwdHf0QRtzLy8u5kIwNh4eH1d+AIOIRmzYPUupGRginmCRwWoExEkJ1ZDKZ8/j4OF8DVBVja2trlRzWLEOsjEFV3t3dzWMQH4nsTVUyB1iTc+pESghXxdXVVXmbjZFEBOQ1tZxM4FQzl/GctwzjxCLZ7EPMjEEFck3Rl3OAyslqrRMpId9POGO0OcGZKOaQuFyTcPdPJpPqO/EbxMoY+U3KGKxtliuPw4AY5iCZ/pxTJzJCSALvnEranFDu+efn5+qdyuE05/ckyXEeksm1swxxUwgQm32ppmxzZVGBXJm0kU+7blYihI8z1UAC+LeXO5wkZz+nmATSR6I5rY1GI6bT6cK1xBjJ/i6Rdo5nPPZB5M7OTpVk+qk0+nJvoHKotNFotLBPnaxEiPk/FiKGhYhhIWJYiBgWIoaFiGEhYliIGBYihoWIYSFiWIgYFiKGhYhhIWJYiBgWIoaFiGEhYliIGBYihoWIYSFiWIgYFiKGhYhhIWJYiBgWIoaFiGEhYliIGBYihoWIYSFiWIgYFiKGhYhhIWJYiBgWIoaFiGEhYliIGBYihoWIYSFiWIgYFiLGPxfY2Bvll5LhAAAAAElFTkSuQmCC)

By default, the `placeholder` shortcode creates 100x100 pixel images in the PNG format. You can customize the size and format of the image by providing parameters to the shortcode.

## Usage

The `placeholder` shortcode can take additional arguments controling the size and format of the image:

``` markdown
{{< placeholder 400 200 format=svg >}}
```

![](data:image/svg+xml;base64,PHN2ZyB3aWR0aCA9ICI0MDAiIGhlaWdodCA9ICIyMDAiIHhtbG5zID0gImh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Qm94ID0gIjAgMCA0MDAgMjAwIj48cmVjdCB3aWR0aCA9ICI0MDAiIGhlaWdodCA9ICIyMDAiIGZpbGwgPSAiI2RkZCIgLz48dGV4dCB4ID0gIjUwJSIgeSA9ICI1MCUiIGZvbnQtZmFtaWx5ID0gInNhbnMtc2VyaWYiIGZvbnQtc2l6ZSA9ICIyMCIgZmlsbCA9ICIjMDAwIiB0ZXh0LWFuY2hvciA9ICJtaWRkbGUiPjQwMCB4IDIwMDwvdGV4dD48L3N2Zz4=)

This will create a scalable vector graphic (SVG) placeholder image with dimensions of 400x200 pixels.

It also takes an optional `format` keyword argument.

- `{{< placeholder >}}`: Create a 100x100 pixel PNG placeholder image.
- `{{< placeholder width >}}`: Create a `width`x`width` pixel PNG placeholder image.
- `{{< placeholder width height >}}`: Create a `width`x`height` pixel PNG placeholder image.
- `{{< placeholder format="svg" >}}`: Create a 100x100 SVG placeholder image.
- `{{< placeholder width format="svg" >}}`: Create a `width`x`width` SVG placeholder image.
- `{{< placeholder width height format="svg" >}}`: Create a `width`x`height` SVG placeholder image.
