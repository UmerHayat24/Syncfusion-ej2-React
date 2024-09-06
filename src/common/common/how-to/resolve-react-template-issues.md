# Resolve Syncfusion React UI Components' Template issues

The React property of `delayUpdate` is used to solve the react template related issues.

## delayUpdate

The `delayUpdate` property enables the delay when the component renders back after the state is changed.

Whenever the state changes, the component and the template renders back. Thus, the react will not allow multiple mounting at the same time. In this situation, React renders the template as an external component, and delays the component re-rendering to compile the template.

By setting the `delayUpdate` property to `true`, the component renders back after the template compilation is done.

```typescript

 <ScheduleComponent width='100%' height='650px' delayUpdate='true'> </ScheduleComponent>

 ```