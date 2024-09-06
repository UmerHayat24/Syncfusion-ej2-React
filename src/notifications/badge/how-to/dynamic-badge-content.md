# Dynamic badge content

Badges in real-time needs to be updated dynamically based on the requirements. In this sample, using React `states`
the badges content will be updated dynamically. Click the increment button to change the badge value.

{% tab template="badge/dynamic-badge", isDefaultActive=true, compileJsx=true %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

interface IBadgeValuesProps {
    BadgeType: string;
    BadgeContent: string;
}


class BadgePortable extends React.Component<IBadgeValuesProps, {}> {
    constructor(props: any) {
        super(props);
    }

    public render() {
        return (
            <span className={this.props.BadgeType}
                style={{ float: 'right', marginTop: '16px', fontSize: '12px' }}>{this.props.BadgeContent} New
            </span>
        );
    }
}

interface IBadgeValues {
    Primary: number;
    Social: number;
    Promotions: number;
    Updates: number;
    Important: number;
    Drafts: number;
}

class App extends React.Component<any, IBadgeValues> {
    constructor(data: any) {
        super(data);
        this.state = {
            Primary: 3,
            Social: 27,
            Promotions: 7,
            Updates: 13,
            Drafts: 7,
            Important: 2
        }
    }

    // Datasource for listview, badge field is the class data for Badges
    public dataSource: { [key: string]: Object }[] = [
        { id: 'p_01', text: 'Primary', badge: 'e-badge e-badge-primary', icons: 'primary', type: 'Primary' },
        { id: 'p_02', text: 'Social', badge: 'e-badge e-badge-secondary', icons: 'social', type: 'Primary' },
        { id: 'p_03', text: 'Promotions', badge: 'e-badge e-badge-success', icons: 'promotion', type: 'Primary' },
        { id: 'p_04', text: 'Updates', badge: 'e-badge e-badge-info', icons: 'updates', type: 'Primary' },
        { id: 'p_05', text: 'Starred', badge: '', icons: 'starred', type: 'All Labels' },
        { id: 'p_06', text: 'Important', badge: 'e-badge e-badge-danger', icons: 'important', type: 'All Labels' },
        { id: 'p_07', text: 'Sent', badge: '', icons: 'sent', type: 'All Labels' },
        { id: 'p_08', text: 'Outbox', badge: '', icons: 'outbox', type: 'All Labels' },
        { id: 'p_09', text: 'Drafts', badge: 'e-badge e-badge-warning', icons: 'draft', type: 'All Labels' },
    ];

    // Map fields
    public fields: object = { groupBy: 'type' };

    public listTemplate(data: any): JSX.Element {
        return (
            <div className='listWrapper' style={{ width: 'inherit', height: 'inherit' }}>
                <span className={`${data.icons} list_svg`}>&nbsp;</span>
                <span className='list_text'>{data.text}</span>
                {
                    data.badge !== '' ?
                        <BadgePortable BadgeContent={(this.state as any)[data.text]} BadgeType={data.badge} /> : ''
                }
            </div>
        );
    }

    public onClick(): void {
          let badgeElements = Array.prototype.slice.call(document.getElementById('lists').getElementsByClassName('e-badge'));
          badgeElements.forEach((element) => {
          element.textContent = (Number(element.textContent.split(' ')[0])) + 1 + ' New';
        })
    }

    render() {
        return (
            <div className="sample_container badge-list">
                {/* Listview element */}
                <ListViewComponent id="lists" dataSource={this.dataSource} fields={this.fields} headerTitle='Inbox' showHeader={true} template={this.listTemplate.bind(this) as any}></ListViewComponent>
                <p className='crossline'></p>
                <span className='incr_button'>
                    <button className='e-btn e-primary' onClick={this.onClick.bind(this)}>Increment Badge Count</button>
                </span>
            </div>
        );
    }
}
ReactDOM.render(<App />, document.getElementById("element"));
```

{% endtab %}
