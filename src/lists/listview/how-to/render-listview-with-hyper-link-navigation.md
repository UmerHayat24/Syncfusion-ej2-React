# Render ListView with hyper link navigation

We can use `anchor` tag along with `href` attribute in our ListView [`template`](../../api/list-view/#template) property for navigation.

In the below sample, we have rendered `ListView` with search engines URL.

{% tab template="listview/navigation", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css",compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {

//Define an array of JSON data
public dataSource: { [key: string]: Object }[] = [
    { name: 'Google', url: 'https://www.google.com' },
    { name: 'Bing', url: 'https://www.bing.com' },
    { name: 'Yahoo', url: 'https://www.yahoo.com' },
    { name: 'Ask.com', url: 'https://www.ask.com' },
    { name: 'AOL.com', url: 'https://www.aol.com' }
];

anchor_template(data: any): JSX.Element {
    return (
        <a target='_blank' href={data.url}>{data.name}</a>
    )};

    render() {
        return (
        <ListViewComponent id='list'
                dataSource={this.dataSource}
                headerTitle = 'Search engines'
                showHeader = {true}
                template= {this.anchor_template as any} >
                </ListViewComponent>
        )
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
