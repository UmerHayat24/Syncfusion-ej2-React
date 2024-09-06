# Resolve delay rendering of Syncfusion React UI Components

The React property of `immediateRender` is used to solve the rendering delay of Syncfusion React UI Components.

## immediateRender

The `immediateRender` property disables the delay on the initial rendering of the component. By default, we have delayed the component rendering to compile the templates since react will not allow multiple mounting at the same time.

In some cases, the template is not available. In this kind of situation, by setting the `immediateRender` property to `true`, the component will be rendered immediately.

```typescript

 <ButtonComponent immediateRender="true" onClick={() => this.setState({ hideButton: true})}>Click to hide</ButtonComponent>

```

> Note: Enable this property only if there is no template in the React UI Component.