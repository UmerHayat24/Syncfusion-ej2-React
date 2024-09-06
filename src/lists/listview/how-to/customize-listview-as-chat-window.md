# Customize ListView as Chat Window

ListView can be customizable as chat window. To achieve that, use ListView [template](../../api/list-view/#template) property and [Avatar](../../avatar/getting-started) component.

    * Listview template property is used to showcase the ListView as chat window.
    * Avatar component is used to design the image of contact person.

Refer the below template code snippet for Template of chat window.

{% tab compileJsx=true%}

```typescript
public listTemplate(data: any): JSX.Element {
        let sendertemplate = <div className='settings'><div id="content"><div className="name">{data.text}</div><div id="info">{data.contact}</div></div>{
                    data.avatar !== "" ?
                        <div id="image"><span className='e-avatar img1 e-avatar-circle'>{data.avatar}</span></div> : <div id="image"><span className={`${data.pic} img1 e-avatar e-avatar-circle`}></span></div>
                }</div>
        let receivertemplate = <div className='settings'>{
                    data.avatar !== "" ?
                        <div id="image2"><span className='e-avatar img2 e-avatar-circle'>{data.avatar}</span></div> : <div id="image2"><span className={`${data.pic} img2 e-avatar e-avatar-circle`}></span></div>
                }<div id="content1"><div className="name1">{data.text}</div><div id="info1">{data.contact}</div></div></div>


        return (
            <div>
                {data.chat !== "receiver" ? (sendertemplate) : (receivertemplate)}
            </div>
        );
    }
```

{% endtab %}

## Chat order in template

In ListView template, we have rendered the list items based on receiver and sender information from dataSource of listview.

## Adding messages to chat window

    * Use textbox to get message from user.
    * Add the textbox message to ListView dataSource using [addItem](../../api/list-view/#additem) method.

{% tab compileJsx=true%}

```typescript

btnClick() {
    let value = this.textboxEle.value;
    this.listObj.addItem([{ text: "Amenda", contact: value, id: "2", avatar: "A", pic: "", chat: "receiver" }]);
    this.textboxEle.value ="";
}

```

{% endtab %}

{% tab template="listview/chat-window", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';

export default class App extends React.Component<{}, {}> {
  listObj: ListViewComponent = null as any;
  textboxEle: any;
  //Define an array of JSON data
  data: { [key: string]: Object }[] = [
    {
      text: "Jenifer",
      contact: "Hi",
      id: "1",
      avatar: "",
      pic: "pic01",
      chat: "sender"
    },
    { text: "Amenda", contact: "Hello", id: "2", avatar: "A", pic: "", chat: "receiver" },
    {
      text: "Jenifer",
      contact: "What Knid of application going to launch",
      id: "4",
      avatar: "",
      pic: "pic01",
      chat: "sender"
    },
    {
      text: "Amenda ",
      contact: "A knid of Emergency broadcast App",
      id: "5",
      avatar: "A",
      pic: "",
      chat: "receiver"
    },
    {
      text: "Jacob",
      contact: "Can you please elaborate",
      id: "6",
      avatar: "",
      pic: "pic04",
      chat: "sender"
    }
  ];

  listTemplate(data: any): JSX.Element {
    const sendertemplate = (
      <div className="settings">
        <div id="content">
          <div className="name">{data.text}</div>
          <div id="info">{data.contact}</div>
        </div>
        {data.avatar !== "" ? (
          <div id="image">
            <span className="e-avatar img1 e-avatar-circle">{data.avatar}</span>
          </div>
        ) : (
          <div id="image">
            <span className={`${data.pic} img1 e-avatar e-avatar-circle`} />
          </div>
        )}
      </div>
    );

    const receivertemplate = (
      <div className="settings">
        {data.avatar !== "" ? (
          <div id="image2">
            <span className="e-avatar img2 e-avatar-circle">{data.avatar}</span>
          </div>
        ) : (
          <div id="image2">
            <span className={`${data.pic} img2 e-avatar e-avatar-circle`} />
          </div>
        )}
        <div id="content1">
          <div className="name1">{data.text}</div>
          <div id="info1">{data.contact}</div>
        </div>
      </div>
    );

    return <div>{data.chat !== "receiver" ? sendertemplate : receivertemplate}</div>;
  }

  btnClick() {
    const value = this.textboxEle.value;
    this.listObj.addItem([
      { text: "Amenda", contact: value, id: "2", avatar: "A", pic: "", chat: "receiver" }
    ]);
    this.textboxEle.value = "";
  }

  render() {
    return (
      <div>
        {/* ListView element */}
        <ListViewComponent
          id="List"
          dataSource={this.data}
          headerTitle="Chat"
          showHeader={true}
          template={this.listTemplate as any}
          ref={scope => {
            this.listObj = scope as any;
          }}
        />

        <input
          id="inputname"
          className="e-input"
          ref={textbox => {
            this.textboxEle = textbox;
          }}
          type="text"
          placeholder="Type your message"
        />

        <ButtonComponent id="btn" onClick={this.btnClick.bind(this)}>
          Send
        </ButtonComponent>
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
