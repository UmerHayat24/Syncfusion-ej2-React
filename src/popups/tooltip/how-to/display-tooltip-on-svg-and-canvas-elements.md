# Display tooltip on SVG and canvas elements

Tooltip can be displayed on both SVG and Canvas elements. You can directly attach the `<svg>` or `<canvas>` elements to show tooltips on data visualization elements.

## SVG

Create the SVG square element and refer to the following code snippet to render the tooltip on SVG square.

```tsx
  <TooltipComponent content='SVG Square' cssClass='e-tooltip-css' target= '#square'>
  </TooltipComponent>
```

## Canvas

Create the canvas circle element and refer to the following code snippet to render the tooltip on Canvas circle.

```tsx
<TooltipComponent content='Canvas Circle' cssClass='e-tooltip-css' target= '#circle'>
  </TooltipComponent>
```

{% tab template="tooltip/svg-canvas", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

{% endtab %}
