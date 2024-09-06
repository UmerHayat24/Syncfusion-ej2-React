---
title: "Load content through Ajax"
component: "Tab"
description: "This example demonstrates how to load external content into the Essential JS 2 Tab control through an AJAX post."
---

# Load content through Ajax

The Tab supports to load external contents through `AJAX` library. Refer to the following steps.

* Import the `Ajax` module from `ej2-base` and initialize with URL path.

* Get the data from Ajax `Success` event, then initialize the Tab with retrieved external path data.

{% tab template="tab/tab-ajax", compileJsx=true %}

```typescript

import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { TabComponent, TabItemDirective, TabItemsDirective } from '@syncfusion/ej2-react-navigations';
import { Ajax } from '@syncfusion/ej2-base';


export default class App extends React.Component<{}, {}> {
    // define the array of data
      render() {
           let headertext: any;
    headertext = [{ text: "Twitter"}, { text: "Facebook"}, { text: "WhatsApp"}];

    return (
          <TabComponent heightAdjustMode='Auto' id='tabelement'>
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
                content= { this.props.data} />
            </TabItemsDirective>
          </TabComponent>
    );
  }
}
let ajax: Ajax = new Ajax('./ajax.html', 'GET', true);
ajax.send().then();
ajax.onSuccess = (dataSt: string): void => {
ReactDOM.render(<App data={dataSt} />, document.getElementById("element") as HTMLElement); }

```

{% endtab %}
