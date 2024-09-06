# Manipulate ListView as Grid Layout

In Listview, list items can be rendered in grid layout with following data manipulations.

* Add Item

* Remove Item

* Sort Items

* Filter Items

## Grid Layout

In this section, we will discuss about rendering of list items in grid layout.

* Initialize and render ListView with dataSource which will render list items in list layout.

* Now, add the below CSS to list item. This will make list items to render in grid layout

```css

#default-list .e-list-item {
        height: 100px;
        width: 100px;
        float: left;
}

```

In the below sample, we have rendered List items in grid layout.

{% tab template="listview/grid-layout", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';

export default class App extends React.Component<{}, {}> {

    //Define an array of number
   public data: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9];

listtemplate(data: any): JSX.Element {
    return (
        <img id="listImage" src="./apple.png" alt="apple" />
    )};

    render() {
        return (
        <ListViewComponent id='list'
                dataSource={this.data}
                template= {this.listtemplate as any} >
                </ListViewComponent>
        )
    }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}

## Data manipulation

In this section, we will discuss about ListView data manipulations.

### Add Item

We can add list item using [`addItem`](../../api/list-view/#additem) API. This will accept array of data as argument.

```typescript

 this.listViewInstance.addItem([{text: 'Apricot', id: '32'}]);

```

In the below sample, you can add new fruit item by clicking add button which will open dialog box with fruit name and image URL text box. After entering the item details, click the add button. This will add your new fruit item.

### Remove item

We can remove list item using [`removeItem`](../../api/list-view/#removeitem) API. This will accept fields with `id` or list item element as argument.

```typescript

 this.listViewInstance.removeItem({id: '32'});

```

In the below sample, you can remove fruit by hovering the fruit item which will show delete button and click that delete button to delete that fruit from your list.

### Sort Items

Listview can be sorted either in Ascending or Descending order. To enable sorting in your ListView, set [`sortOrder`](../../api/list-view/#sortorder) as `Ascending` or `Descending`.

```typescript

<ListViewComponent id='list' sortOrder= 'Ascending'></ListViewComponent>

```

We can also set sorting after component initialization.

```typescript

this.listViewInstance.sortOrder = 'Ascending'

```

In the below sample, we have sorted fruits in `Ascending` order. To sort it in descending, click on sort order icon and vice versa.

### Filter Items

Listview data can be filtered with the help of [`dataManager`](https://ej2.syncfusion.com/react/documentation/data/getting-started/). After filtering the data, update ListView [`dataSource`](https://ej2.syncfusion.com/react/documentation/api/list-view/#datasource) with filtered data.

```typescript

let value = this.filterInput.value;  //input text box value
let filteredData = new DataManager(this.listdata).executeLocal(
        new Query().where("text", "startswith", value, true)
);

this.listViewInstance.dataSource = filteredData;

```

In the below sample, we can filter fruit items with the help of search text box. This will filter fruit items based on your input. Here we used [`startswith`](https://ej2.syncfusion.com/react/documentation/data/querying/#filter-operators) of input text to filter data in DataManager.

{% tab template="listview/manipulation", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css", compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { ListViewComponent } from '@syncfusion/ej2-react-lists';
import { closest, enableRipple, MouseEventArgs } from '@syncfusion/ej2-base';
import { DataManager, Query } from "@syncfusion/ej2-data";
import { DialogComponent } from '@syncfusion/ej2-react-popups';

export default class App extends React.Component<{}, {}> {
  public ascClass: string = "e-sort-icon-ascending";
  public desClass: string = "e-sort-icon-descending";
  //Define an array of JSON data
  public fruitsdata: { [key: string]: Object }[] = [
    { text: "Date", id: "1", imgUrl: "./dates.jpg" },
    { text: "Fig", id: "2", imgUrl: "./fig.jpg" },
    { text: "Apple", id: "3", imgUrl: "./apple.png" },
    { text: "Apricot", id: "4", imgUrl: "./apricot.jpg" },
    { text: "Grape", id: "5", imgUrl: "./grape.jpg" },
    { text: "Strawberry", id: "6", imgUrl: "./strawberry.jpg" },
    { text: "Pineapple", id: "7", imgUrl: "./pineapple.jpg" },
    { text: "Melon", id: "8", imgUrl: "./melon.jpg" },
    { text: "Lemon", id: "9", imgUrl: "./lemon.jpg" },
    { text: "Cherry", id: "10", imgUrl: "./cherry.jpg" }
  ];

  public add: HTMLElement | null = null;
  public search: HTMLInputElement | null = null;
  public sort: HTMLElement | null = null;
  public imgURL: HTMLInputElement | null = null;
  public name: HTMLInputElement | null = null;
  public dialogInstance: DialogComponent | null = null;
  public listviewInstance: ListViewComponent | null = null;
  public buttonObj = [
    {
      click: this.dlgButtonClick.bind(this),
      buttonModel: { content: "Add", isPrimary: true }
    }
  ];

  addItem() {
    if (this.name) this.name.value = "";
    if (this.imgURL) this.imgURL.value = "";
    if (this.dialogInstance) this.dialogInstance.show();
  }

  //Here we are removing list item
  onDeleteBtnClick(e: any) {
    e.stopPropagation();
    let li: Element = closest(e.currentTarget, ".e-list-item");
    let data = (this.listviewInstance as any).findItem(li);
    (this.listviewInstance as any).removeItem(data);
    new DataManager(this.fruitsdata).remove("id", { id: data["id"] });
  }

  //Here we are adding list item
  dlgButtonClick() {
    if (this.listviewInstance && this.dialogInstance) {
      let name: string = (this.name as any).value;
      let url: string = (this.imgURL as any).value;
      let id: number = Math.random() * 10000;
      this.listviewInstance.addItem([{ text: name, id: id, imgUrl: url }]);
      this.fruitsdata.push({ text: name, id: id, imgUrl: url });
      this.dialogInstance.hide();
    }
  }

  //Here we are sorting list item
  sortItems() {
    if (this.listviewInstance && this.sort) {
      let ele = this.sort.firstElementChild as HTMLElement;
      let des = ele.classList.contains(this.desClass) ? true : false;
      if (des) {
        ele.classList.remove(this.desClass);
        ele.classList.add(this.ascClass);
        this.listviewInstance.sortOrder = "Ascending";
      } else {
        ele.classList.remove(this.ascClass);
        ele.classList.add(this.desClass);
        this.listviewInstance.sortOrder = "Descending";
      }
      this.listviewInstance.dataBind();
    }
  }

  //Here, the list items are filtered using the DataManager instance.
  onKeyUp() {
    if (this.listviewInstance) {
      let value: string = (this.search as any).value;
      let data: Object[] = new DataManager(this.fruitsdata).executeLocal(
        new Query().where("text", "startswith", value, true)
      );
      if (!value) {
        this.listviewInstance.dataSource = this.fruitsdata.slice();
      } else {
        this.listviewInstance.dataSource = data as { [key: string]: Object }[];
        this.listviewInstance.dataBind();
      }
    }
  }

  content(data: any): JSX.Element {
    return (
      <div id="listDialog">
        <div className="input_name">
          <label htmlFor="name">Fruit Name: </label>
          <input
            id="name"
            ref={scope => {
              this.name = scope;
            }}
            className="e-input"
            type="text"
            placeholder="Enter fruit name"
          />
        </div>
        <div>
          <label htmlFor="imgurl">Fruit Image: </label>
          <input
            id="imgurl"
            ref={scope => {
              this.imgURL = scope;
            }}
            className="e-input"
            type="text"
            placeholder="Enter image url"
          />
        </div>
      </div>
    );
  }

  listtemplate(data: any): JSX.Element {
    return (
      <div className="fruits">
        <div className="first">
          <img id="listImage" src={data.imgUrl} alt="fruit" />
          <button
            className="delete e-control e-btn e-small e-round e-delete-btn e-primary e-icon-btn"
            data-ripple="true"
          >
            <span
              className="e-btn-icon e-icons delete-icon"
              onClick={this.onDeleteBtnClick.bind(this)}
            />
          </button>
        </div>
        <div className="fruitName">{data.text}</div>
      </div>
    );
  }

  render() {
    return (
      <div id="container">
        <div className="headerContainer">
          <div className="e-input-group">
            <input
              id="search"
              ref={scope => {
                this.search = scope;
              }}
              className="e-input"
              type="text"
              onKeyUp={this.onKeyUp.bind(this)}
              placeholder="Search fruits"
            />
            <span className="e-input-group-icon e-input-search" />
          </div>

          <button
            id="sort"
            className="e-control e-btn e-small e-round e-primary e-icon-btn"
            ref={scope => {
              this.sort = scope;
            }}
            title="Sort fruits"
            onClick={this.sortItems.bind(this)}
            data-ripple="true"
          >
            <span className="e-btn-icon e-icons e-sort-icon-ascending" />
          </button>

          <button
            id="add"
            className="e-control e-btn e-small e-round e-primary e-icon-btn"
            ref={scope => {
              this.add = scope;
            }}
            onClick={this.addItem.bind(this)}
            title="Add fruit"
            data-ripple="true"
          >
            <span className="e-btn-icon e-icons e-add-icon" />
          </button>
        </div>

        <ListViewComponent
          id="list"
          dataSource={this.fruitsdata.slice()}
          template={this.listtemplate.bind(this) as any}
          sortOrder="Ascending"
          ref={scope => {
            this.listviewInstance = scope;
          }}
        />

        <DialogComponent
          id="dialog"
          header="Add fruit"
          content={this.content.bind(this) as any}
          visible={false}
          buttons={this.buttonObj}
          ref={dialog => (this.dialogInstance = dialog)}
          width={"300px"}
          showCloseIcon={true}
        />
      </div>
    );
  }
}
ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
