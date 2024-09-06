---
title: "Tooltip Content"
component: "Tooltip"
description: "React tooltip component's content can be assigned with static text, template, or loaded dynamically via AJAX."
---

# Content

A text or a piece of information assigned to the Tooltip's `content` property will be displayed as the main text stream of the Tooltip.
 It can be a string or a template content. If the `content` property is not provided with any specific value, then it takes the value
  assigned to the `title` attribute of the target element on which the Tooltip was initialized. The content can also dynamically be
   assigned to the Tooltip via AJAX.

## Template content

Any text or image can be added to the Tooltip, by default. To customize the Tooltip layout or to create your own visualized element on the
 Tooltip, template can be used.

Refer to the following code example to add formatted HTML content to the Tooltip.

{% tab template="tooltip/content-1", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```tsx
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent } from '@syncfusion/ej2-react-popups';

class App extends React.Component<{}, {}> {
  private content() {
    return(
      <div id='tooltipContent'>
      <p><strong>Environmentally friendly</strong> or <strong>environment-friendly</strong>, <i>(also referred to as eco-friendly, nature-friendly, and green)</i> are marketing and sustainability terms referring to goods and services, laws, guidelines and policies that inflict reduced, minimal, or no harm upon ecosystems or the environment.</p></div>
    )
  }
  render() {
    let style: object = {
      display: 'inline-block',
      padding : '5px'
    };
    return (
        <p>A green home is a type of house designed to be
            <TooltipComponent width="300px" height="60px" isSticky={true} content={this.content} style={style}>
            <a><u>environmentally friendly</u></a>
            </TooltipComponent> and sustainable. And also focuses on the efficient use of "energy, water, and building materials." As green homes
            have become more prevalent we have also seen the emergence of green affordable housing.
        </p>
    );
  }
}
ReactDom.render(<App />,document.getElementById('sample'));

```

{% endtab %}

## Dynamic content via AJAX

The Tooltip content can be dynamically loaded  by making use of the AJAX call. The AJAX request is usually made within the `beforeRender`
 event of the Tooltip, and then the Tooltip's `content` is assigned the value retrieved on it's success.

{% tab template="tooltip/ajax-content", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,tooltipdata.json", compileJsx=true %}

```javascript
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { TooltipComponent, TooltipEventArgs } from '@syncfusion/ej2-react-popups';
import { Ajax } from '@syncfusion/ej2-base';

class App extends React.Component<{}, {}> {
  private tooltipInstance: TooltipComponent;
  public onBeforeRender(args: TooltipEventArgs): void {
    this.tooltipInstance.content = 'Loading...';
    this.tooltipInstance.dataBind();
    let ajax: Ajax = new Ajax('./tooltipdata.json', 'GET', true);
    ajax.send().then(
      (result: any) => {
        result = JSON.parse(result);
        for (let i: number = 0; i < result.length; i++) {
          if (result[i].Id === args.target.getAttribute('data-content')) {
            this.tooltipInstance.content = "<div class='contentWrap'>" + result[i].Sports + "</div>";
          }
        }
        this.tooltipInstance.dataBind();
      },
      (reason: any) => {
        this.tooltipInstance.content = reason.message;
        this.tooltipInstance.dataBind();
      });
  }
  render() {
    return (
      <div id="container">
        <h4>National Sports</h4>
        <TooltipComponent id="targetContainer" ref={t => this.tooltipInstance = t} className="e-prevent-select" content="Loading..." target=".target" position="RightCenter" beforeRender={this.onBeforeRender.bind(this)}>
          <div id="countrylist">
            <ul>
              <li className="target" title="1"><span>Australia</span></li>
              <li className="target" title="2"><span>Bhutan</span></li>
              <li className="target" title="3"><span>China</span></li>
              <li className="target" title="4"><span>Cuba</span></li>
              <li className="target" title="5"><span>India</span></li>
              <li className="target" title="6"><span>Switzerland</span></li>
              <li className="target" title="7"><span>United States</span></li>
            </ul>
          </div>
        </TooltipComponent>
      </div>
    );
  }
}
ReactDom.render(<App />, document.getElementById('sample'));

```

{% endtab %}
