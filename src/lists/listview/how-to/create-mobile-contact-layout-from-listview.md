# Create Mobile Contact layout from ListView

You can customize the ListView using the
[template](../../api/list-view/#template) property. Refer
to the following steps to customize ListView as mobile contact view with our `ej2-avatar`.

* Render the ListView with
[dataSource](../../api/list-view/#datasource) that has
avatar data. You can set avatar data as either text or class names. Refer to the following codes.

{% tab compileJsx=true%}

```typescript

let dataSource = [
  {
    text: "Jenifer", contact: "(206) 555-985774", id: "1", avatar: "", pic: "pic01"
  },
  {
    text: "Amenda", contact: "(206) 555-3412", id: "2", avatar: "A", pic: ""
  }
];

```

{% endtab %}

* Set `avatar` classes in ListView template to customize contact icon. In the following codes, medium size avatar has been
set using the class name `e-avatar e-avatar-circle` from data source.

{% tab compileJsx=true%}

```typescript

 public listTemplate(data): JSX.Element {
    let letterAvatar = <span className='e-avatar e-avatar-circle'>{data.avatar}</span>
    let imageAvatar = <span className={`${data.pic} e-avatar e-avatar-circle`}></span>

    return (
        <div className='e-list-wrapper e-list-multi-line e-list-avatar'>
            {data.avatar !== "" ? (letterAvatar) : (imageAvatar)}
            <span className="e-list-content">{data.contact}</span>
        </div>
    );
}

```

{% endtab %}

> Avatars can be set in different sizes in avatar classes. To know more about avatar classes, refer to
[Avatar](https://ej2.syncfusion.com/react/demos/#/material/avatar/default).

* Sort the contact names using the
[`sortOder`](../../api/list-view/#sortorder) property of ListView.

* Enable the [`showHeader`](../../api/list-view/#showheader)
property, and set the
[`headerTitle`](../../api/list-view/#headertitle)
as `Contacts`.

{% tab template="listview/avatar", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript
import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {
      //Define an array of JSON data
    public data: { [key: string]: Object }[] = [
        { id: 's_01', text: 'Robert', avatar: '', pic: 'pic04' },
        { id: 's_02', text: 'Nancy', avatar: 'N', pic: '' },
        { id: 's_05', text: 'Jenifer', pic: 'pic01', avatar: '' },
        { id: 's_03', text: 'Andrew', avatar: 'A', pic: '' },
        { id: 's_06', text: 'Margaret', pic: 'pic02', avatar: '' },
        { id: 's_07', text: 'Steven', pic: 'pic03', avatar: '' },
        { id: 's_08', text: 'Michael', avatar: 'M', pic: '' }
    ];

    public fields: any = { text: "Name" };

    public listTemplate(data: any): JSX.Element {
        let letterAvatar = <span className='e-avatar e-avatar-circle'>{data.avatar}</span>
        let imageAvatar = <span className={`${data.pic} e-avatar e-avatar-circle`}></span>

        return (
            <div className='e-list-wrapper e-list-avatar'>
                {data.avatar !== "" ? (letterAvatar) : (imageAvatar)}
                <span className="e-list-content">{data.text}</span>
            </div>
        );
    }

    render() {
        return (
           <div>
                {/* ListView element */}
                <ListViewComponent id='list' dataSource={this.data} headerTitle='Contacts' showHeader={true}
                    sortOrder="Ascending" width='350px' template={this.listTemplate as any}
                    fields={this.fields as any} cssClass='e-list-template'></ListViewComponent>
            </div>

        );
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
