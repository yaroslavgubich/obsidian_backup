In CSS, you can set the size of an image using the `width` and `height` properties. Here's how you can do it:

### Setting Width and Height Directly:

```css
img {
  width: 300px;   /* Set the width to 300 pixels */
  height: 200px;  /* Set the height to 200 pixels */
}
```

### Setting Width and Having the Height Adjust Automatically:

If you only set the `width` (or only the `height`), the other dimension (height or width, respectively) will be adjusted automatically to maintain the image's aspect ratio.

```css
img {
  width: 50%;   /* Set the width to 50% of its container */
}
```

### Using `max-width` and `max-height`:

These properties are useful to ensure that an image never exceeds a certain size, but can be smaller if the aspect ratio dictates it.

```css
img {
  max-width: 100%;   /* Ensure the image never exceeds the width of its container */
  height: auto;      /* This will maintain the aspect ratio */
}
```

### Background Images:

If you're dealing with background images (set with `background-image` property), you can control their size with the `background-size` property:

```css
div {
  background-image: url('path-to-image.jpg');
  background-size: cover;   /* Resize the background image to cover the entire container, might be cropped */
}
```

Other values for `background-size` include:
- `contain`: Resize the background image to make sure the image is fully visible.
- Specific values like `300px 200px`: Width and height respectively.

### Important Considerations:

1. **Aspect Ratio**: If you set both `width` and `height`, this could distort the image if the aspect ratio isn't the same as the original image. To maintain the aspect ratio, you can set either `width` or `height` and then set the other to `auto`.

2. **Performance**: Large images that are resized using CSS could still have a large file size. It's a good practice to resize the image to a suitable dimension before using it in a web page, especially if it's significantly larger than its display size.

3. **Responsive Design**: Consider using relative units like percentages (`%`) or viewport units (`vw`, `vh`) for image sizes in responsive designs. This ensures images scale appropriately across different screen sizes and resolutions.
