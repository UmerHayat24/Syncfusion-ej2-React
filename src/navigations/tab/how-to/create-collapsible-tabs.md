---
title: "Create collapsible Tabs"
component: "Tab"
description: "This example demonstrates how to create tabs in a collapsible state when they are initially rendered in the Essential JS 2 Tab control."
---

# Create collapsible Tabs

You can achieve collapse and expand functionality in Tab by adding/removing a custom CSS class in the click event handler for each tab.
* Define a CSS class to set the style property display as none. Here 'collapse' class is added to the content element for hiding it using [`created`](../../api/tab#created) event.
* Bind the [`selected`](../../api/tab#selected) event for Tab to collapse the initially selected Tab item and bind custom click handler for the Tab headers.
* In the event handler, add and remove 'collapse' class to hide and show the corresponding Tab content.

{% tab template="tab/collapse", sourceFiles="app/**/*.tsx,index.css", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TabComponent, TabItemDirective, TabItemsDirective, SelectEventArgs } from '@syncfusion/ej2-react-navigations';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

export default class App extends React.Component<{}, {}> {
  public tabInstance:TabComponent | null;
  public prevIndex: number = 0;
  public trgIndex: number;
  public actLine: HTMLElement;

  constructor() {
    super(PeriodicWave);
    this.updateCollapseClass = this.updateCollapseClass.bind(this);
  }

  public updateCollapseClass(index: number): void {
    // Custom classes are added/removed from tab content and active line element, when the same tab item again clicked
    const cntEle: any = document.getElementById("e-content_" + index);
    if (cntEle.classList.contains('collapse')) {
        cntEle.classList.remove('collapse');
        this.actLine.classList.remove('collapse');
    } else {
        cntEle.classList.add('collapse');
        this.actLine.classList.add('collapse');
    }
}

  public tabCreated(): void {
    // After tab created first tab content and active line are hidden by adding custom class
    this.actLine = document.querySelector('.e-indicator') as any;
    (document.getElementById("e-content_0") as any).classList.add('collapse');
    this.actLine.classList.add('collapse');
  }

  public tabSelected(e: SelectEventArgs): void {
    // If next tab item selected custom class is removed from content and active line element
    let cnttrgs: NodeListOf<Element> = document.querySelectorAll('#element.e-tab > .e-content > .e-item');
    for (let i: number = 0; i < cnttrgs.length; i++) {
      cnttrgs[i].classList.remove('collapse');
    }
    if (this.actLine !== undefined) { this.actLine.classList.remove('collapse'); }
    this.trgIndex = e.selectedIndex;
    e.selectedItem.onclick = (e : Event) => {
      this.updateCollapseClass(this.trgIndex);
    };
  }

  render() {
    let headertext: any;
    headertext = [{ text: "Twitter"}, { text: "Facebook"}, { text: "WhatsApp"}];

    return (
      <TabComponent heightAdjustMode='Auto' className="e-background" id='element' ref={tab => this.tabInstance = tab} created={this.tabCreated}  selected= {this.tabSelected.bind(this)}>
        <TabItemsDirective>
          <TabItemDirective header= { headertext[0] }
            content= { 'Twitter is an online social networking service that enables users to send and read short 140-character ' +
            'messages called "tweets". Registered users can read and post tweets, but those who are unregistered can only read ' +
            'them. Users access Twitter through the website interface, SMS or mobile device app Twitter Inc. is based in San ' +
            'Francisco and has more than 25 offices around the world. Twitter was created in March 2006 by Jack Dorsey, ' +
            'Evan Williams, Biz Stone, and Noah Glass and launched in July 2006. The service rapidly gained worldwide popularity, ' +
            'with more than 100 million users posting 340 million tweets a day in 2012.The service also handled 1.6 billion ' +
            'search queries per day.' } />
          <TabItemDirective header= { headertext[1] }
            content= { 'Facebook is an online social networking service headquartered in Menlo Park, California. Its website was ' +
            'launched on February 4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo ' +
            'Saverin, Andrew McCollum, Dustin Moskovitz and Chris Hughes.The founders had initially limited the website\'\s ' +
            'membership to Harvard students, but later expanded it to colleges in the Boston area, the Ivy League, and Stanford ' +
            'University. It gradually added support for students at various other universities and later to high-school students.' } />
          <TabItemDirective header= { headertext[2] }
            content= { 'WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates ' +
            'under a subscription business model. It uses the Internet to send text messages, images, video, user location and ' +
            'audio media messages to other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user ' +
            'base of up to one billion,[10] making it the most globally popular messaging application. WhatsApp Inc., based in ' +
            'Mountain View, California, was acquired by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.' } />
        </TabItemsDirective>
      </TabComponent>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
