---
title: "Set custom animation"
component: "Accordion"
description: "This example demonstrates how to set custom animation for expand and collapse actions in the Essential JS 2 Accordion control."
---

# Set custom animation

Accordion supports custom animations for both expand and collapse actions from the provided animation option of `Animation` library.  The [`animation`](../../api/accordion#animation) property also allows you to set [`easing`](../../api/accordion/accordionActionSettingsModel#easing), [`duration`](../../api/accordion/accordionActionSettingsModel#duration), and various other effects of your choice.

Default animation is given as `SlideDown` for expanding the panel using [`expand`](../../api/accordion/accordionAnimationSettingsModel#expand) animation property and `SlideUp` for collapsing the panel using [`collapse`](../../api/accordion/accordionAnimationSettingsModel#collapse) animation property. You can also disable the animation by setting animation [`effect`](../../api/accordion/accordionActionSettingsModel#effect) as `none`.

The sample demonstrates some types of animation that suits for Accordion. You can check all the animation effects here.

{% tab template="accordion/accordion-custom", compileJsx=true %}

```typescript
import { Effect } from '@syncfusion/ej2-base';
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { AccordionComponent, AccordionItemDirective, AccordionItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';


export class ReactApp extends React.Component<{}, {}> {
  public acrdnInstance:AccordionComponent;
  public expandInstance:DropDownListComponent;
  public collapseInstance:DropDownListComponent;
  private expandAni: string[] = ['SlideDown', 'SlideUp', 'FadeIn', 'FadeOut', 'FadeZoomIn', 'FadeZoomOut', 'ZoomIn', 'ZoomOut', 'None'];
  
  constructor(props: any) {
    super(props);
    this.collapseAnimationChange = this.collapseAnimationChange.bind(this);
    this.expandAnimationChange = this.expandAnimationChange.bind(this);
  }

  public content0() {
    return <div>
     Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web services. ASP.NET pages execute on the server and generate markup such as HTML, WML, or XML that is sent to a desktop or mobile browser. ASP.NET pages use a compiled,event-driven programming model that improves performance and enables the separation of application logic and user interface.
      </div>;
  }
  public content1() {
    return <div>
      The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model, the view, and the controller. The ASP.NET MVC framework provides an alternative to the ASP.NET Web Forms pattern for creating Web applications. The ASP.NET MVC framework is a lightweight, highly testable presentation framework that (as with Web Forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication.
      </div>;
  }
  public content2() {
    return <div>
     JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter the document content that was displayed.More recently, however, it has become common in both game development and the creation of desktop applications.
      </div>;
  }
  public collapseAnimationChange(e : ChangeEventArgs): void {

    this.acrdnInstance.animation.collapse = { effect: this.collapseInstance.value as Effect}
  }
  public expandAnimationChange(e : ChangeEventArgs): void {
    this.acrdnInstance.animation.expand = { effect: this.expandInstance.value as Effect}
  }

  public render() {
    const wrapStyle = { padding: '25px 0 0' };
    return (
       <div style={wrapStyle}>
        <div className='row'>
          <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <label> Expand Animation </label>
          </div>
          <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <DropDownListComponent ref={expand => this.expandInstance = expand!} index = '0' change={this.expandAnimationChange} dataSource={this.expandAni} popupHeight="250px" placeholder="Select Expand animation" />
          </div>
        </div>
        <div className='row'>
          <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <label> Collapse Animation </label>
          </div>
          <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <DropDownListComponent ref={collapse => this.collapseInstance = collapse!} index = '1' change={this.collapseAnimationChange} dataSource={this.expandAni} popupHeight="250px" placeholder="Select Collapse animation" />
          </div>
        </div>

        <AccordionComponent ref={acrdn => this.acrdnInstance = acrdn!}>
              <AccordionItemsDirective>
                <AccordionItemDirective header='ASP.NET' content={this.content0} />
                <AccordionItemDirective header='ASP.NET MVC' content={this.content1} />
                 <AccordionItemDirective header='Javascript' content={this.content2} />
              </AccordionItemsDirective>
            </AccordionComponent>
      </div>
    );
  }
}

ReactDOM.render(<ReactApp />, document.getElementById("element"));
```

{% endtab %}
