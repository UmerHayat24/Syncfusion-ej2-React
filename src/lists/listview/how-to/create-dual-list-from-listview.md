# Create Dual List from ListView

The dual list contains two ListView. This allows you to move list items from one list to another using the client-side
events. This section explains how to integrate the ListView component to achieve dual list.

## Use cases

* Stock exchanges of two different countries
* Job applications (skill sets)

## Integration of Dual List

Here, two ListView components have been used to display the list items. An ej2-button is used to transfer data between
the ListView, and a textbox is used to achieve the UI of filtering support.

The dual list supports:

* Moving whole data from one list to another.
* Moving selected data from one list to another.
* Filtering the list by using a client-side typed character.

In the ListView component, sorting is enabled using the
[sortOrder](../../api/list-view/#sortorder) property, and
the [select](../../api/list-view/#select) event is triggered
while selecting an item. Here, the select event is triggered to enable and disable button states.

## Manipulating data

## Moving whole data from the first list to the second list(>>)

* Here, the whole data can be moved from the first ListView to the second by clicking the first button. When clicking the button,
the whole list items are sliced, and `concat` with the second ListView. This button is enabled only when the data source
of the first ListView is not empty.

## Moving whole data from the second list to the first list(<<)

* The functionality of the second button is the same as above, and data is transferred from the second list to the first
list. This button is enabled only when the data source of the second ListView is not empty.

## Moving selected item from one list to another list (>) and (<)

* The [Select](../../api/list-view/#select) event is triggered
when selecting a list item in the ListView. The selected items can be transferred between two lists. These buttons will be
enabled when selecting an item in lists.

## Filtering method

* The filtering method is used to filter list items when typing a character in the text box. In this
method, the [`dataManager`](https://ej2.syncfusion.com/react/documentation/data/getting-started/) has been
used to fetch data from the data source and display in ListView.

## Sorting

* By using the dual list, list items can be sorted in the ListView component using the
[sortOrder](../../api/list-view/#sortorder) property.
You can enable sorting in one ListView; in the same order, data can be transferred to another ListView.

{% tab template="listview/dual-list", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true%}

```typescript

import * as React from 'react';
import * as ReactDOM from "react-dom";
import { DataManager, Query } from '@syncfusion/ej2-data';
import { enableRipple } from "@syncfusion/ej2-base";
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { ButtonComponent } from '@syncfusion/ej2-react-buttons';
enableRipple(true);

export default class App extends React.Component<{}, {}> {
  //Define an array of JSON data
  firstListData: any[] = [
    { text: "Hennessey Venom", id: "list-01" },
    { text: "Bugatti Chiron", id: "list-02" },
    { text: "Bugatti Veyron Super Sport", id: "list-03" },
    { text: "SSC Ultimate Aero", id: "list-04" },
    { text: "Koenigsegg CCR", id: "list-05" },
    { text: "McLaren F1", id: "list-06" }
  ];

  secondListData: any[] = [
    { text: "Aston Martin One- 77", id: "list-07" },
    { text: "Jaguar XJ220", id: "list-08" },
    { text: "McLaren P1", id: "list-09" },
    { text: "Ferrari LaFerrari", id: "list-10" }
  ];
  firstInput: HTMLInputElement | null = null;
  secondInput: HTMLInputElement | null = null;
  listFirstInstance: ListViewComponent | null = null;
  listSecondInstance: ListViewComponent | null = null;
  firstBtnInstance: ButtonComponent | null = null;
  secondBtnInstance: ButtonComponent | null = null;
  thirdBtnInstance: ButtonComponent | null = null;
  fourthBtnInstance: ButtonComponent | null = null;

  componentDidMount() {
    if (this.listFirstInstance && this.listSecondInstance) {
      this.firstListData = (this.listFirstInstance.dataSource as any[]).slice();
      this.secondListData = (this.listSecondInstance.dataSource as any[]).slice();
    }
  }

  //Map the appropriate columns to fields property
  fields: Object = { text: "text", id: "id" };

  onFirstListSelect() {
    if (this.secondBtnInstance) this.secondBtnInstance.disabled = false;
  }

  onSecondListSelect() {
    if (this.thirdBtnInstance) this.thirdBtnInstance.disabled = false;
  }

  updateFirstListData() {
    if (this.listFirstInstance) {
      Array.prototype.forEach.call(
        (this.listFirstInstance as any).liCollection as any[],
        (list: any) => {
          this.firstListData.forEach((data, index) => {
            if (list.innerText.trim() === data.text) {
              delete this.firstListData[index];
            }
          });
        }
      );
      if (this.firstInput) {
        this.firstInput.value = "";
      }
      let ds: any[] = [];
      this.firstListData.forEach(data => {
        ds.push(data);
      });
      this.firstListData = ds;
    }
  }

  updateSecondListData() {
    Array.prototype.forEach.call((this.listSecondInstance as any).liCollection, (list: any) => {
      this.secondListData.forEach((data, index) => {
        if (list.innerText.trim() === data.text) {
          delete this.secondListData[index];
        }
      });
    });
    if (this.secondInput) {
      this.secondInput.value = "";
    }
    let ds: any[] = [];
    this.secondListData.forEach(data => {
      ds.push(data);
    });
    this.secondListData = ds;
  }

  onFirstKeyUp(e: any) {
    if (this.firstInput) {
      let value = this.firstInput.value;
      var data = new DataManager(this.firstListData).executeLocal(
        new Query().where("text", "startswith", value, true)
      );
      if (this.listFirstInstance) {
        if (!value) {
          this.listFirstInstance.dataSource = this.firstListData.slice();
        } else {
          this.listFirstInstance.dataSource = data as any[];
        }
        this.listFirstInstance.dataBind();
      }
    }
  }

  onSecondKeyUp(e: any) {
    if (this.secondInput) {
      let value = this.secondInput.value;
      var data = new DataManager(this.secondListData).executeLocal(
        new Query().where("text", "startswith", value, true)
      );
      if (this.listSecondInstance) {
        if (!value) {
          this.listSecondInstance.dataSource = this.secondListData.slice();
        } else {
          this.listSecondInstance.dataSource = data as any[];
        }
        this.listSecondInstance.dataBind();
      }
    }
  }

  setButtonState() {
    if (
      this.listFirstInstance &&
      this.firstBtnInstance &&
      this.secondBtnInstance &&
      this.listSecondInstance &&
      this.fourthBtnInstance &&
      this.thirdBtnInstance
    ) {
      if ((this.listFirstInstance.dataSource as any[]).length) {
        this.firstBtnInstance.disabled = false;
      } else {
        this.firstBtnInstance.disabled = true;
        this.secondBtnInstance.disabled = true;
      }

      if ((this.listSecondInstance.dataSource as any[]).length) {
        this.fourthBtnInstance.disabled = false;
      } else {
        this.fourthBtnInstance.disabled = true;
        this.thirdBtnInstance.disabled = true;
      }
    }
  }

  firstBtnClick() {
    if (this.listFirstInstance && this.firstBtnInstance && this.listSecondInstance) {
      this.listSecondInstance.dataSource = Array.prototype.concat.call(
        this.listFirstInstance.dataSource,
        this.listSecondInstance.dataSource
      );
      this.updateFirstListData();
      this.listFirstInstance.removeMultipleItems((this.listFirstInstance as any).liCollection);
      this.firstListData = this.firstListData.concat(this.listFirstInstance.dataSource);
      this.secondListData = this.listSecondInstance.dataSource.slice();
      this.firstBtnInstance.disabled = true;
      this.onFirstKeyUp(null);
      this.setButtonState();
    }
  }

  secondBtnClick() {
    if (this.listFirstInstance && this.secondBtnInstance && this.listSecondInstance) {
      let e = this.listFirstInstance.getSelectedItems();
      if (e) {
        this.listSecondInstance.dataSource = Array.prototype.concat.call(
          this.listSecondInstance.dataSource,
          e.data
        );
        this.listFirstInstance.removeItem(e.item as any);
        this.firstListData = this.listFirstInstance.dataSource as any[];
        this.secondListData = this.listSecondInstance.dataSource.slice();
        this.onFirstKeyUp(null);
        this.secondBtnInstance.disabled = true;
        this.setButtonState();
      }
    }
  }

  thirdBtnClick() {
    if (this.listFirstInstance && this.listSecondInstance && this.thirdBtnInstance) {
      let e = this.listSecondInstance.getSelectedItems();
      if (e) {
        this.listFirstInstance.dataSource = Array.prototype.concat.call(
          this.listFirstInstance.dataSource,
          e.data
        );
        this.listSecondInstance.removeItem(e.item as any);
        this.secondListData = this.listSecondInstance.dataSource as any[];
        this.firstListData = this.listFirstInstance.dataSource.slice();
        this.onSecondKeyUp(null);
        this.thirdBtnInstance.disabled = true;
        this.setButtonState();
      }
    }
  }

  fourthBtnClick() {
    if (this.listFirstInstance && this.listSecondInstance && this.fourthBtnInstance) {
      this.listFirstInstance.dataSource = Array.prototype.concat.call(
        this.listFirstInstance.dataSource,
        this.listSecondInstance.dataSource
      );
      this.updateSecondListData();
      this.listSecondInstance.removeMultipleItems((this.listSecondInstance as any).liCollection);
      this.secondListData = this.secondListData.concat(this.listSecondInstance.dataSource);
      this.firstListData = this.listFirstInstance.dataSource.slice();
      this.onSecondKeyUp(null);
      this.setButtonState();
    }
  }

  firstInputKeyUp() {
    if (
      this.listFirstInstance &&
      this.firstBtnInstance &&
      this.secondBtnInstance &&
      this.listSecondInstance &&
      this.fourthBtnInstance &&
      this.thirdBtnInstance &&
      this.firstInput
    ) {
      let value = this.firstInput.value;
      var data = new DataManager(this.firstListData).executeLocal(
        new Query().where("text", "startswith", value, true)
      );
      if (!value) {
        this.listFirstInstance.dataSource = this.firstListData.slice();
      } else {
        this.listFirstInstance.dataSource = data as any[];
      }
      this.listFirstInstance.dataBind();
    }
  }

  secondInputKeyUp() {
    if (
      this.listFirstInstance &&
      this.firstBtnInstance &&
      this.secondBtnInstance &&
      this.listSecondInstance &&
      this.fourthBtnInstance &&
      this.thirdBtnInstance &&
      this.secondInput
    ) {
      let value = this.secondInput.value;
      var data = new DataManager(this.secondListData).executeLocal(
        new Query().where("text", "startswith", value, true)
      );
      if (!value) {
        this.listSecondInstance.dataSource = this.secondListData.slice();
      } else {
        this.listSecondInstance.dataSource = data as any[];
      }
      this.listSecondInstance.dataBind();
    }
  }

  render() {
    return (
      <div id="container">
        <div className="col-lg-12 control-section">
          <div>
            <h3>Dual List</h3>
            <div id="text1">
              <input
                className="e-input"
                type="text"
                id="firstInput"
                ref={(inputRef: any) => (this.firstInput = inputRef)}
                placeholder="Filter"
                onKeyUp={this.firstInputKeyUp.bind(this)}
                title="Type in a name"
              />
            </div>
            <ListViewComponent
              id="list-1"
              dataSource={this.firstListData}
              fields={this.fields}
              sortOrder="Ascending"
              select={this.onFirstListSelect.bind(this)}
              ref={scope => {
                this.listFirstInstance = scope;
              }}
            />
            <div id="btn">
              <ButtonComponent
                onClick={this.firstBtnClick.bind(this)}
                ref={button1 => {
                  this.firstBtnInstance = button1;
                }}
              >
                {" "}
                >>{" "}
              </ButtonComponent>
              <ButtonComponent
                onClick={this.secondBtnClick.bind(this)}
                ref={button2 => {
                  this.secondBtnInstance = button2;
                }}
              >
                {" "}
                >{" "}
              </ButtonComponent>
              <ButtonComponent
                onClick={this.thirdBtnClick.bind(this)}
                ref={button3 => {
                  this.thirdBtnInstance = button3;
                }}
              >
                {" "}
                {"<"}{" "}
              </ButtonComponent>
              <ButtonComponent
                onClick={this.fourthBtnClick.bind(this)}
                ref={button4 => {
                  this.fourthBtnInstance = button4;
                }}
              >
                {" "}
                {"<<"}{" "}
              </ButtonComponent>
            </div>
            <div id="text2">
              <input
                className="e-input"
                type="text"
                onKeyUp={this.secondInputKeyUp.bind(this)}
                id="secondInput"
                ref={(inputRef: any) => (this.secondInput = inputRef)}
                placeholder="  Filter"
                title="Type in a name"
              />
            </div>
            <ListViewComponent
              id="list-2"
              dataSource={this.secondListData}
              fields={this.fields}
              sortOrder="Ascending"
              select={this.onSecondListSelect.bind(this)}
              ref={list => {
                this.listSecondInstance = list;
              }}
            />
          </div>
        </div>
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));
```

{% endtab %}
