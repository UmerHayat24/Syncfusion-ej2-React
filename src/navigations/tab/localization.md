---
title: "Tab Localization"
component: "Tab"
description: "Tab localization section explains how to localize the tab based on culture and set close button's tooltip text."
---

# Localization

Localization library allows to localize the default text content of the Tab to different cultures using the [`locale`](../api/tab#locale) property. In Tab, the close button's tooltip text alone will be localize based on culture.  The close button is shown on tab header when enabled [`showCloseButton`](../api/tab#showclosebutton) property.

| Locale key | en-US (default)  |
|------|------|
| closeButtonTitle |  Close |

## Loading translations

To load translation object in an application use `load` function of `L10n` class.

In the below sample, `French` culture is set to Tab and change the close button's tooltip
text.

{% tab template="tab/locale", compileJsx=true  %}

```typescript

import { L10n } from '@syncfusion/ej2-base';
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

L10n.load({
  'fr-BE': {
    'tab': {
      'closeButtonTitle': "Fermer"
    }
  }
});

export default class ReactApp extends React.Component<{}, {}> {
  public headerText: any = [{ text: "HTML" }, { text: "C Sharp(C#)" }, { text: "Java" }];

  public content0() {
    return <div>
      HyperText Markup Language, commonly referred to as HTML, is the standard markup language used to create web pages. Along with CSS, and JavaScript, HTML is a cornerstone technology, used by most websites to create visually engaging web pages, user interfaces for web applications, and user interfaces for many mobile applications.[1] Web browsers can read HTML files and render them into visible or audible web pages. HTML describes the structure of a website semantically along with cues for presentation, making it a markup language, rather than a programming language.
      </div>;
  }
  public content1() {
    return <div>
      C# is intended to be a simple, modern, general-purpose, object-oriented programming language. Its development team is led by Anders Hejlsberg. The most recent version is C# 5.0, which was released on August 15, 2012.
      </div>;
  }
  public content2() {
    return <div>
      Java is a set of computer software and specifications developed by Sun Microsystems, later acquired by Oracle Corporation, that provides a system for developing application software and deploying it in a cross-mobile phones to platform computing environment. Java is used in a wide variety of computing platforms from embedded devices and enterprise servers and supercomputers. While less common, Java applets run in secure, sandboxed environments to provide many features of native applications and can be embedded in HTML pages.
      </div>;
  }

  public render() {
    return (
      <TabComponent heightAdjustMode='Auto' locale="fr-BE" showCloseButton={true}>
        <TabItemsDirective>
          <TabItemDirective header={this.headerText[0]} content={this.content0} />
          <TabItemDirective header={this.headerText[1]} content={this.content1} />
          <TabItemDirective header={this.headerText[2]} content={this.content2} />
        </TabItemsDirective>
      </TabComponent>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}