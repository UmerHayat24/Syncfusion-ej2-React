# Show items count in Group Header

The ListView component supports wrapping list items into a group based on the category. The category of each list item can
be mapped with groupBy field of the data source. You can display grouped list items count in the list-header using the group
header template. Refer to the following code sample to display grouped list item count.

{% tab template="listview/item-count", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {

        //Define an array of JSON data
    private data: { [key: string]: Object }[]  = [
        { Name: 'Nancy', contact:'(206) 555-985774', id: '1', image: 'https://ej2.syncfusion.com/demos/src/grid/images/1.png',  category: 'Experience'},
        { Name: 'Janet', contact: '(206) 555-3412', id: '2', image: 'https://ej2.syncfusion.com/demos/src/grid/images/3.png', category: 'Fresher' },
        { Name: 'Margaret', contact:'(206) 555-8122', id:'4', image: 'https://ej2.syncfusion.com/demos/src/grid/images/4.png', category: 'Experience' },
        { Name: 'Andrew ', contact:'(206) 555-9482', id: '5', image: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', category: 'Experience'},
        { Name: 'Steven', contact:'(71) 555-4848', id: '6', image: 'https://ej2.syncfusion.com/demos/src/grid/images/5.png', category: 'Fresher' },
        { Name: 'Michael', contact:'(71) 555-7773', id: '7', image: 'https://ej2.syncfusion.com/demos/src/grid/images/6.png', category: 'Experience' },
        { Name: 'Robert', contact:'(71) 555-5598', id: '8', image: 'https://ej2.syncfusion.com/demos/src/grid/images/7.png', category: 'Fresher' },
        { Name: 'Laura', contact:'(206) 555-1189', id: '9', image: 'https://ej2.syncfusion.com/demos/src/grid/images/8.png', category: 'Experience' },
    ];

    private fields: object =  { text: 'Name', groupBy: 'category' };
     //Set customized list template
    listTemplate(data: any): JSX.Element {
        return(
            <div className="e-list-wrapper e-list-multi-line e-list-avatar">
                <img className="e-avatar e-avatar-circle" src={data.image} />
                <span className="e-list-item-header">{data.Name}</span>
                <span className="e-list-content">{data.contact}</span>
            </div>
        );
    }
    //Set customized group-header template
    groupTemplate(data: any): JSX.Element {
        return(
            <div><span className='category'>{data.items[0].category}</span><span className="count"> {data.items.length} Item(s)</span></div>
        );
    }
    render() {
        return (
            <div>
                <ListViewComponent id='list' dataSource={this.data} fields={this.fields} template={this.listTemplate as any} groupTemplate={this.groupTemplate as any} cssClass='e-list-template'></ListViewComponent>
            </div>
        );
    }
}

ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
