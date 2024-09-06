---
title: "Set custom animation"
component: "Tab"
description: "This example demonstrates how to set custom animation for both previous and next actions on Essential JS 2 Tab component when the tab select."
---

# Set custom animation

Tab supports custom animations for both previous and next actions from the provided animation option of `Animation` library. The [`animation`](../../api/tab#animation) property also allows you to set [`easing`](../../api/tab/tabActionSettings#easing), [`duration`](../../api/tab/tabActionSettings#duration), and various other [`effect`](../../api/tab/tabActionSettings#effect).

Default animation is given as `SlideLeftIn` for [`previous`](../../api/tab/tabAnimationSettingsModel#previous) tab animation and `SlideRightIn` for [`next`](../../api/tab/tabAnimationSettingsModel#next) tab animation. You can also disable the animation by setting the animation effect as `None`. Also, please use the following CSS to disable indicator animation for animation effect as `None`.

```CSS

.e-tab .e-tab-header:not(.e-vertical) .e-indicator, .e-tab .e-tab-header.e-vertical .e-indicator {
    transition: none;
}

```

The sample demonstrates some types of animation that suits Tab. You can check all the animation effects here.

{% tab template="tab/persistence", compileJsx=true %}

```typescript
import { Effect } from '@syncfusion/ej2-base';
import { ChangeEventArgs, DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import * as React from 'react';
import * as ReactDOM from 'react-dom';

export default class ReactApp extends React.Component<{}, {}> {
  public headerText: any = [{ text: "Twitter" }, { text: "Facebook" }, { text: "WhatsApp" }];
  public tabInstance: TabComponent;
  public previousInstance: DropDownListComponent;
  public nextInstance: DropDownListComponent;
  private animationData: string[] = ['SlideLeftIn', 'SlideRightIn', 'FadeIn', 'FadeOut', 'FadeZoomIn', 'FadeZoomOut', 'ZoomIn', 'ZoomOut', 'None'];
  
  constructor(props: any) {
    super(props);
    this.previousAnimationChange = this.previousAnimationChange.bind(this);
    this.nextAnimationChange = this.nextAnimationChange.bind(this);
  }

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
  public previousAnimationChange(): void {
    this.tabInstance.animation.previous = { effect: this.previousInstance.value as Effect };
  }
  public nextAnimationChange(): void {
    this.tabInstance.animation.next = { effect: this.nextInstance.value as Effect };
  }

  public render() {
    const wrapStyle = { padding: '25px 0 0' };
    return (
       <div style={wrapStyle}>
        <div className='row'>
          <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <label> Previous Animation </label>
          </div>
          <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <DropDownListComponent ref={previous => this.previousInstance = previous!} index='0' change={this.previousAnimationChange} dataSource={this.animationData} popupHeight="250px" placeholder="Select Previous animation" />
          </div>
        </div>
        <div className='row'>
          <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <label> Next Animation </label>
          </div>
          <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <DropDownListComponent ref={next => this.nextInstance = next!} index='1' change={this.nextAnimationChange} dataSource={this.animationData} popupHeight="250px" placeholder="Select Next animation" />
          </div>
        </div>
      <TabComponent ref={tab => this.tabInstance = tab!}>
        <TabItemsDirective>
          <TabItemDirective header={this.headerText[0]} content={this.content0} />
          <TabItemDirective header={this.headerText[1]} content={this.content1} />
          <TabItemDirective header={this.headerText[2]} content={this.content2} />
        </TabItemsDirective>
      </TabComponent>
      </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById('element'));

```

{% endtab %}