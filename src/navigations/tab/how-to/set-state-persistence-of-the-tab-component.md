---
title: "Set state persistence of the Tab component"
component: "Tab"
description: "This example demonstrates how to retain the current model value in the browser cookies for state maintenance of the Essential JS 2 Tab component."
---

# Set state persistence of the Tab component

State persistence allows the Tab to retain the current modal value in the browser cookies for state maintenance. This action is handled through the [`enablePersistence`](../../api/tab#enablepersistence) property which is set to false by default.
When it is set to true, some of the Tab component model values will be retained even after refreshing the page.

The following sample demonstrates how to set state persistence of the Tab component.

{% tab template="tab/persistence", compileJsx=true %}

```typescript
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class ReactApp extends React.Component<{}, {}> {
  public headerText: any = [{ text: "Twitter" }, { text: "Facebook" }, { text: "WhatsApp" }];

  public content0() {
    return <div>
      Twitter is an online social networking service that enables users to send and read short 140-character messages called "tweets". Registered users can read and post tweets, but those who are unregistered can only read them. Users access Twitter through the website interface, SMS or mobile device app Twitter Inc. is based in San Francisco and has more than 25 offices around the world. Twitter was created in March 2006 by Jack Dorsey, Evan Williams, Biz Stone, and Noah Glass and launched in July 2006. The service rapidly gained worldwide popularity, with more than 100 million users posting 340 million tweets a day in 2012.The service also handled 1.6 billion search queries per day.
      </div>;
  }
  public content1() {
    return <div>
      Facebook is an online social networking service headquartered in Menlo Park, California. Its website was launched on February 4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo Saverin, Andrew McCollum, Dustin Moskovitz and Chris Hughes.The founders had initially limited the website membership to Harvard students, but later expanded it to colleges in the Boston area, the Ivy League, and Stanford University. It gradually added support for students at various other universities and later to high-school students.
      </div>;
  }
  public content2() {
    return <div>
      WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates under a subscription business model. It uses the Internet to send text messages, images, video, user location and audio media messages to other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user base of up to one billion,[10] making it the most globally popular messaging application. WhatsApp Inc., based in Mountain View, California, was acquired by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.
      </div>;
  }

  public render() {
    return (
      <TabComponent heightAdjustMode='Auto' enablePersistence={true}>
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
