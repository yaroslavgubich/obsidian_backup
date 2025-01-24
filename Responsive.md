Certainly! Here's a guideline for when to use responsive units (`%`, `rem`, etc.) versus fixed units (`px`):
Where to use REM EM, %, pixels ?
### Use Responsive Units (`%`, `rem`, etc.):

1. **Layout Containers**: Elements that serve as main containers for your content, especially if you want the layout to adapt to different screen sizes.
    - Example: Main content wrappers, sidebars, and grids.

2. **Font Sizes**: To ensure readability and accessibility across devices.
    - Example: Paragraph text, headings, and other textual content.

3. **Spacing**:
    - **Margins and Paddings**: Especially for elements within a fluid container. This ensures consistent spacing regardless of screen size.

4. **Responsive Images**: To ensure that images resize appropriately across devices without causing layout issues.
    - Example: Images within an article or a responsive gallery.

5. **Modals or Overlays**: Elements that should scale based on the viewport size, especially when they should be consistent in appearance across devices.

6. **UI Elements within a Fluid Container**:
    - Example: Buttons, form elements, and cards within a responsive container.

7. **Flexible Grid Systems**: When using a grid layout that should adapt to varying screen sizes.

### Use Pixels (`px`):

1. **Borders**: A 1px or 2px border should remain consistent across devices.

2. **Icons**: Icons often have specific sizes to ensure clarity and crispness, especially if they are sprite-based.

3. **Specifically Sized Containers**: Elements that should remain the same size regardless of the viewport.
    - Example: Fixed-size modals or pop-ups.

4. **Shadows and Effects**: Things like `box-shadow` offsets or `text-shadow` might be best defined in pixels to ensure they look consistent across screen sizes.

5. **Background Images with Specific Sizes**: If you have a repeating background pattern, it often makes sense to define its size in pixels.

6. **Scrollbars and Custom Scroll Behaviors**: These are often defined in pixels for precise behavior.

7. **Specific Component States**: For example, a dropdown with a fixed height or a slider with a fixed width.

8. **Media Queries**: While it's common to use `em` units for media queries to tie into typography, pixels remain a popular choice for defining breakpoints.

Remember, these are general guidelines. The specifics of your design, the content, and the user experience you aim to provide might lead you to make exceptions. Always test on different devices and screen sizes to ensure your design looks and functions as intended.