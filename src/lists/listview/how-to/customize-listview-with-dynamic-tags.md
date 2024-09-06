# Customize ListView with dynamic tags

You can customize the ListView items using the
[`template`](../../api/list-view/#template) property. Here,
the dynamic tags are added and removed in the list item from another ListView. Refer to the following steps to achieve this.

* Render the ListView with data source, and add button element with each list item of ListView on
[`actionComplete`](../../api/list-view/#actioncomplete) event.
Refer to the following code sample of actionComplete event.

{% tab compileJsx=true%}

```typescript

// The actionComplete event for first ListView to add the button

addButton(args) {
    let buttonObj = { obj: ButtonComponent, prop: { iconCss: 'e-icons e-add-icon', cssClass: 'e-small e-round' } };
    let ele = document.getElementsByClassName("e-but");
    for (let i: number = 0; i < ele.length; i++) {
        buttonObj.obj = new ButtonComponent(buttonObj.prop);
        buttonObj.obj.appendTo(ele[i]);
    }
}

```

{% endtab %}

* Initialize dynamic ListView with required property that holds the tags of parent ListView, and bind the
[`select`](../../api/list-view/#select) event
(triggers when the list item is selected), in which you can get and add the selected item value as tags into parent
ListView. Refer to the following code sample.

{% tab compileJsx=true%}

```typescript

//Select the event that is is rendered inside dialog for ListView
addTag(e) {
    let listTag = document.createElement('span');
    listTag.className = 'advanced-option';
    let labelElem = document.createElement('span');
    labelElem.className = 'label';
    let deleteElem = document.createElement('span');
    deleteElem.className = 'delete';
    deleteElem.onclick = this.removeTag;
    labelElem.innerHTML = e.target.textContent;
    listTag.appendChild(labelElem);
    listTag.appendChild(deleteElem);
    let tag = document.createElement('span');
    tag.className = 'advanced-option-list';
    tag.appendChild(listTag);
    this.listviewInstance.element.querySelector('.e-active').appendChild(tag);
}

```

{% endtab %}

* Render the dialog component with empty content and append the created dynamic ListView object to the dialog on
[`created`](../../api/dialog#created) event.

* Bind the click event for button icon (+) to update the ListView data source with tags, and open the dialog with this
dynamic ListView. Refer to the following code sample.

{% tab compileJsx=true%}

```typescript

//Method to hide/show the dialog and update the ListView data source
renderDialog(id) {
    if (document.getElementsByClassName('e-popup-open').length !== 0) {
        this.dialogInstance.hide();
    }
    else {
         let listElem: any = document.getElementById('dialog').querySelector("#list");
        let listIns = document.getElementById('dialog').querySelector("#list") && document.getElementById('dialog').querySelector("#list").ej2_instances && document.getElementById('dialog').querySelector("#list").ej2_instances[0] ? document.getElementById('dialog').querySelector("#list").ej2_instances[0] : undefined;
        if(listIns){
        listIns.dataSource = this.datasource[id];
        listIns.fields = this.fields;
        listIns.addEventListener('select', ()=> { this.addTag(event);});
        listIns.dataBind();
        listIns.appendTo(listElem);
        this.dialogInstance.position = { X: document.querySelector('.e-add-icon').getBoundingClientRect().left + 50, Y: document.querySelector('.e-add-icon').getBoundingClientRect().top - 5 };
        this.dialogInstance.show();
        }
    }
}

```

{% endtab %}

* Bind the click event with added dynamic tags to remove it. Refer to the following code sample.

```typescript

//Method to remove the list item
removeTag() {
    this.parentNode.parentNode.remove();
}

```

{% tab template="listview/dynamic-tag", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import { Browser, EventHandler } from "@syncfusion/ej2-base";

export default class App extends React.Component<{}, {}> {
  //Define an array of JSON data
  public data: any[] = [
    { Id: "Brooke", Name: "Brooke" },
    { Id: "Claire", Name: "Claire" },
    { Id: "Erik", Name: "Erik" },
    { Id: "Grace", Name: "Grace" },
    { Id: "Jacob", Name: "Jacob" }
  ];

  public fields: object = { text: "Name" };
  public position: any = null;
  public animation: object = { effect: "None" };
  public dialogInstance: DialogComponent | null = null;
  public listviewInstance: ListViewComponent | null = null;
  public brookeTag: object[] = [
    { id: "list11", Name: "Discover Music" },
    { id: "list12", Name: "Sales and Events" },
    { id: "list13", Name: "Categories" },
    { id: "list14", Name: "MP3 Albums" },
    { id: "list15", Name: "More in Music" }
  ];

  public claireTag: object[] = [
    { id: "list21", Name: "Songs" },
    { id: "list22", Name: "Bestselling Albums" },
    { id: "list23", Name: "New Releases" },
    { id: "list24", Name: "Bestselling Songs" }
  ];

  public erikTag: object[] = [
    { id: "list31", Name: "Artwork" },
    { id: "list32", Name: "Abstract" },
    { id: "list33", Name: "Acrylic Mediums" },
    { id: "list34", Name: "Creative Acrylic" },
    { id: "list35", Name: "Canvas Art" }
  ];

  public graceTag: object[] = [
    { id: "list41", Name: "Rock" },
    { id: "list42", Name: "Gospel" },
    { id: "list43", Name: "Latin Music" },
    { id: "list44", Name: "Jazz" }
  ];

  public jacobTag: object[] = [
    { id: "list51", Name: "100 Albums" },
    { id: "list52", Name: "Hip-Hop and R&B Sale" },
    { id: "list53", Name: "CD Deals" }
  ];

  public datasource: any = {
    Brooke: this.brookeTag,
    Claire: this.claireTag,
    Erik: this.erikTag,
    Grace: this.graceTag,
    Jacob: this.jacobTag
  };
  dialogListInstance: any;

  renderDialog(id: any) {
    if (document.getElementsByClassName("e-popup-open").length !== 0) {
      if (this.dialogInstance) this.dialogInstance.hide();
    }
    if (this.dialogInstance) {
      let listElem: any = this.dialogInstance.element.querySelector("#list");
      this.dialogListInstance =
        listElem && listElem.ej2_instances && listElem.ej2_instances[0]
          ? listElem.ej2_instances[0]
          : undefined;
      if (this.dialogListInstance) {
        EventHandler.remove(this.dialogListInstance, "select", this.addTag);
        this.dialogListInstance.dataSource = this.datasource[id];
        this.dialogListInstance.fields = this.fields;
        EventHandler.add(this.dialogListInstance, "select", this.addTag, this);
        this.dialogListInstance.appendTo(listElem);
        this.dialogListInstance.dataBind();
        this.dialogInstance.position = {
          X:
            (this.listviewInstance as any).element.querySelector(".e-add-icon").getBoundingClientRect()
              .left + 50,
          Y:
            (this.listviewInstance as any).element.querySelector(".e-add-icon").getBoundingClientRect()
              .top - 5
        };
          this.dialogInstance.show();
      }
    }
  }

  addTag(e: any) {
    let listTag = document.createElement("span");
    listTag.className = "advanced-option";
    let labelElem = document.createElement("span");
    labelElem.className = "label";
    let deleteElem = document.createElement("span");
    deleteElem.className = "delete";
    deleteElem.onclick = this.removeTag;
    labelElem.innerHTML = e.text;
    listTag.appendChild(labelElem);
    listTag.appendChild(deleteElem);
    let tag = document.createElement("span");
    tag.className = "advanced-option-list";
    tag.appendChild(listTag);
    (this.listviewInstance as any).element.querySelector(".e-active").appendChild(tag);
  }
  removeTag() {
    (this as any).parentNode.parentNode.remove();
  }

  handleClick(e: any) {
    this.renderDialog(e.currentTarget.id);
  }

  listtemplate(data: any): JSX.Element {
    return (
      <div>
        <span className="templatetext">{data.Name}</span>
        <span className="designationstyle">
          <ButtonComponent
            id={data.Id}
            className="e-but e-small e-round"
            iconCss={"e-icons e-add-icon"}
            onClick={this.handleClick.bind(this)}
          />
        </span>
      </div>
    );
  }

  dialogContent(): JSX.Element {
    return <ListViewComponent id="list" showHeader={true} headerTitle="Favorite" width={"200px"} />;
  }

  render() {
    return (
      <div id="sample">
        <ListViewComponent
          id="template-list"
          dataSource={this.data}
          fields={this.fields}
          template={this.listtemplate.bind(this) as any}
          ref={scope => {
            this.listviewInstance = scope;
          }}
        />
        <DialogComponent
          id="dialog"
          animationSettings={this.animation as any}
          content={this.dialogContent as any}
          visible={false}
          ref={dialog => (this.dialogInstance = dialog)}
          width={"200px"}
          showCloseIcon={true}
          position={this.position}
        />
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
