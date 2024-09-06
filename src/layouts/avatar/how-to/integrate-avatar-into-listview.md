# Integrate avatar into Listview

Avatar is integrated into the listview to create contacts applications. The `xsmall` size avatar is used to match the size
of the list item. Letters and images are also used as avatar content.

{% tab template="avatar/listview", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

class ReactApp extends React.Component<{}, {}> {

    //Define an array of JSON data
    public data: { [key: string]: Object }[] = [
        { id: 's_01', text: 'Robert', avatar: '', pic: 'pic04' },
        { id: 's_02', text: 'Nancy', avatar: 'N', pic: '' },
        { id: 's_05', text: 'John', pic: 'pic01', avatar: '' },
        { id: 's_03', text: 'Andrew', avatar: 'A', pic: '' },
        { id: 's_06', text: 'Margaret', avatar: 'M', pic: 'pic02' },
        { id: 's_07', text: 'Steven', pic: 'pic03', avatar: '' },
        { id: 's_08', text: 'Michael', pic: 'pic02', avatar: '' }
    ];
    public template(data: any): JSX.Element {
        let letterAvatar = <span className='e-avatar e-avatar-small e-avatar-circle'>{data.avatar}</span>
        let imageAvatar = <span className={`${data.pic} e-avatar e-avatar-small e-avatar-circle`}></span>

        return (
            <div className='listWrapper'>
                {data.avatar !== "" ? (letterAvatar) : (imageAvatar)}
                <span className='text'>{data.text}</span>
            </div>
        );
    }

  render() {
       return (
        <div>
            <div className="sample_container listview">
                {/* ListView element */}
                <ListViewComponent cssClass='letterAvatarList' dataSource={this.data} headerTitle='Contacts' showHeader={true}
                    sortOrder="Ascending" template={this.template as any}></ListViewComponent>
            </div>
        </div>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}
