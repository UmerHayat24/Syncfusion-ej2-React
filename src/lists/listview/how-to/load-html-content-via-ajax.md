# Load HTML content via AJAX

We can set external `HTML` page content as [`template`](../../api/list-view/#template) for our `ListView` component by making use of `AJAX` call.

```typescript

        this.ajax = new Ajax('./template.html', 'GET', false);
        this.ajax.onSuccess = (e: string) => {
            this.template = e;
        };
        this.ajax.send();

```

In the below sample, we have rendered smartphone settings template from external `HTML` file.

{% tab template="listview/ajax", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { Ajax } from '@syncfusion/ej2-base';

export default class App extends React.Component<{}, {}> {
  constructor(props: any) {
    super(props);
    this.ajax = new Ajax("./template.html", "GET", false);
    this.ajax.onSuccess = (e: string) => {
      this.template = e;
    };
    this.ajax.send();
  }
  //Define an array of JSON data
  public data: { [key: string]: Object }[] = [
    { name: "Network & Internet", id: "0", description: "Wi-Fi, mobile, data usage, hotspot" },
    { name: "Connected devices", id: "1", description: "Bluetooth, cast, NFC" },
    { name: "Battery", id: "2", description: "18% -4h 12m left" },
    { name: "Display", id: "3", description: "Wallpaper, sleep, font size" },
    { name: "Sound", id: "4", description: "Volume, vibration, Do Not Disturb" },
    { name: "Storage", id: "5", description: "52% used - 15.48 GB free" }
  ];

  public template: any;
  public ajax: Ajax;

  render() {
    return (
      <ListViewComponent
        id="list"
        dataSource={this.data}
        headerTitle="Settings"
        showHeader={true}
        template={this.template}
        cssClass="e-list-template"
      />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
