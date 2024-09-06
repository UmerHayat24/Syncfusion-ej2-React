---
title: "Create wizard using Tab"
component: "Tab"
description: "This online reservation example demonstrates how to create multiple components inside the Essential JS 2 Tab control."
---

# Create wizard using Tab

Tab items can be disabled dynamically by passing the index and boolean value with the [`enableTab`](../../api/tab#enabletab) method and also passing index or HTML element to select an item from the tab using [`select`](../../api/tab#select) method.

Create the following contents for each tab in the wizard.
1. **Search tab:**
   Created with [DropDownList](../../../drop-down-list/data-binding) to select the source, destination and type of ticket. A [DatePicker](../../../datepicker/getting-started/) for choosing the date of journey.
2. **Train tab:**
   Based on the selected start and end point, populated Grid with random list of available seats and train list. Initially define the columns and row selected event for validating, after the source and destination chosen update the [dataSource](../../api/grid#datasource) for the Grid.
3. **Passenger tab:**
   A table with Textbox, Numeric, DropDownList for adding passenger name, age, gender and preferred berth/seat. Add validation on entering passenger details to proceed.
4. **Payment tab:**
   Calculate the ticket cost based on location, passenger count and ticket type. Generate data for Grid with passenger details, train number and ticket cost summary.

You can go back on each tab using buttons available in it and tabs are [`disabled`](../../api/tab/tabItem#disabled) to navigate through tab header click actions. Once you end the wizard all the data get cleared and wizard goes back to starting tab.

In the below demo, designed for simple train reservation module that enable/disable tab items based on sequential validation of each Tab content.

{% tab template="tab/wizard", isDefaultActive=true, compileJsx=true %}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { DropDownListComponent } from '@syncfusion/ej2-react-dropdowns';
import { TabComponent, TabItemDirective, TabItemsDirective, SelectEventArgs } from '@syncfusion/ej2-react-navigations';
import { GridComponent, RowSelectEventArgs, ColumnsDirective, ColumnDirective } from '@syncfusion/ej2-react-grids';

export class App extends React.Component<{}, {}> {
  public alertDlg: DialogComponent;
  public tab: TabComponent;
  public ticketDetailGrid: GridComponent;
  public pass_gender3: DropDownListComponent;
  public pass_gender2: DropDownListComponent;
  public listObj: DropDownListComponent;
  public pass_gender1: DropDownListComponent;
  public pass_berth1: DropDownListComponent;
  public pass_berth2: DropDownListComponent;
  public pass_berth3: DropDownListComponent;
  public pass_age1: NumericTextBoxComponent;
  public availTrainGrid: GridComponent;
  public ticketType: DropDownListComponent;
  public journeyDate: DatePickerComponent;
  public endPoint: DropDownListComponent;
  public startPoint: DropDownListComponent;
  public today: Date = new Date();
  public selectedTrain: any;
  public dlgTarget: HTMLElement = document.querySelector(
    ".sb-content-tab.e-tab .e-content.sb-sample-content-area"
  );
  public dateMin: Date = new Date(this.today.getTime());
  public dateMax: Date = new Date(
    this.today.getTime() + 60 * 24 * 60 * 60 * 1000
  );
  public fields: Object = { id: "id", text: "text", value: "text" };
  public autoCompleteFields: Object = { text: "name", value: "name" };
  public dateValue = new Date();

  public headerText: any = [
    { text: "New Booking" },
    { text: "Train List" },
    { text: "Add Passenger" },
    { text: "Make Payment" }
  ];

  public quotas: any = [
    { id: "1", text: "Business Class" },
    { id: "2", text: "Economy Class" },
    { id: "4", text: "Common Class" }
  ];

  public gender: any = [{ id: "1", text: "Male" }, { id: "2", text: "Female" }];

  public berths: any = [
    { id: "1", text: "Upper" },
    { id: "2", text: "Lower" },
    { id: "3", text: "Middle" },
    { id: "4", text: "Window" },
    { id: "5", text: "Aisle" }
  ];
  public cities: any = [
    { name: "Chicago", fare: 300 },
    { name: "San Francisco", fare: 125 },
    { name: "Los Angeles", fare: 175 },
    { name: "Seattle", fare: 250 },
    { name: "Florida", fare: 150 }
  ];

  public dlgButtons: any = [
    {
      buttonModel: { content: "OK", isPrimary: true },
      // tslint:disable-next-line: no-empty
      click: () => {

     this.alertDlg.hide();
      this.tab.enableTab(0, true);
      this.tab.enableTab(1, false);
      this.tab.enableTab(2, false);
      this.tab.enableTab(3, false);
      this.tab.select(0);
      }
    }
  ];

  public dlgCreated(): void {
    const proxy: any = this;
    proxy.alertDlg.hide();
  }

  public focusIn(): void {
    const proxy: any = this;
    proxy.show();
  }

  public tabSelected(e: SelectEventArgs) {
    if (e.isSwiped) {
      e.cancel = true;
    }
  }

  public trainSelected(args: RowSelectEventArgs): void {
    this.selectedTrain = args.data;
  }

  public btnClicked(e: any): void {
    switch (e.target.id) {
      case "searchNext":
        /* Validate the Source, Destination, Date and Class chosen and proceed only if all the fields are selected */
        if (
          this.startPoint.value != null &&
          this.endPoint.value != null &&
          this.ticketType.value != null &&
          this.journeyDate.value != null
        ) {
          if (
            this.startPoint.value &&
            this.startPoint.value === this.endPoint.value
          ) {
            (document.getElementById("err1") as HTMLElement).innerText =
              "* Arrival point can't be same as Departure";
          } else {
            this.tab.enableTab(0, false);
            this.tab.enableTab(1, true);
            this.filterTrains(e);
            this.tab.select(1);
            (document.getElementById("err1") as HTMLElement).innerText = "";
            if (document.getElementById("err2")) {
              (document.getElementById("err2") as HTMLElement).innerText = "";
            }
          }
        } else {
          (document.getElementById("err1") as HTMLElement).innerText =
            "* Please fill all the details before proceeding";
        }
        break;
      case "bookTickets":
        /* Based on the selected station generate Grid content to display trains available */
        if (
          this.availTrainGrid.getSelectedRecords() === undefined ||
          this.availTrainGrid.getSelectedRecords().length === 0
        ) {
          (document.getElementById("err2") as HTMLElement).innerText =
            "* Select your convenient train";
        } else {
          this.tab.enableTab(2, true);
          this.tab.select(2);
          this.tab.enableTab(1, false);
          (document.getElementById("err2") as HTMLElement).innerText = "";
        }
        break;
      case "confirmTickets":
        /* Get the Passenger details and validate the fields must not be left empty */
        const name: any = document.getElementById("pass_name1");
        const age: any = this.pass_age1.value;
        const gender: any = this.pass_gender1.value;
        if (name.value === "" || age === "" || gender === "") {
          (document.getElementById("err3") as HTMLElement).innerText =
            "* Please enter passenger details";
        } else {
          this.tab.enableTab(3, true);
          this.tab.select(3);
          this.tab.enableTab(2, false);
          (document.getElementById("err3") as HTMLElement).innerText = "";
          this.finalizeDetails(e);
        }
        break;
      case "makePayment":
        this.alertDlg.show();
        break;
      case "goToSearch":
        /* Go back to change class, date or boarding places */
        this.selectedTrain = [];
        this.tab.enableTab(0, true);
        this.tab.select(0);
        this.tab.enableTab(1, false);
        break;
      case "goBackToBook":
        /* Change the preferred train chosen already */
        this.tab.enableTab(1, true);
        this.tab.select(1);
        this.tab.enableTab(2, false);
        break;
      case "goBackDetails":
        /* Update passenger detail before confirming the payment */
        this.tab.enableTab(2, true);
        this.tab.select(2);
        this.tab.enableTab(3, false);
        break;
    }
  }

  public filterTrains(args: RowSelectEventArgs): void {
    /* Generating trains based on source and destination chosen */
    const result: never[] | { [key: string]: Object }[] = [];
    const fromCity: string = this.startPoint.value as string;
    const toCity: string = this.endPoint.value as string;
    const count: number = Math.floor(Math.random() * 3 + 2);

    for (let i: number = 0; i < count; i++) {
      // tslint:disable-next-line: ban-types
      const details: { [key: string]: Object } = {};
      details.TrainNo = Math.floor(Math.random() * 20 + 19000);
      details.Name = "Train " + i;
      details.Departure = fromCity;
      details.Arrival = toCity;
      details.Availability = Math.floor(Math.random() * 20 + 20);
      result.push(details);
    }
    setTimeout(() => {
      this.availTrainGrid.dataSource = result;
      this.availTrainGrid.dataBind();
    }, 100);
  }

  public finalizeDetails(args: RowSelectEventArgs): void {
    /* Get the passenger details and update table with name and other details for confirmation */
    const reserved = [];
    let passCount: any = 0;
    const name1: any = document.getElementById("pass_name1");
    const name2: any = document.getElementById("pass_name2");
    const name3: any = document.getElementById("pass_name3");

    for (let i: number = 1; i <= 3; i++) {
      if (name1.value !== "") {
        // tslint:disable-next-line: ban-types
        const details: { [key: string]: Object } = {};
        const gender: string = (i === 1
          ? this.pass_gender1.value
          : i === 2
          ? this.pass_gender2.value
          : this.pass_gender3.value) as string;
        const berth: string = (i === 1
          ? this.pass_berth1.value
          : i === 2
          ? this.pass_berth2.value
          : this.pass_berth3.value) as string;
        details.TrainNo = this.selectedTrain.TrainNo.toString();
        details.PassName =
          i === 1 ? name1.value : i === 2 ? name2.value : name3.value;
        details.Gender = gender === "" ? "Male" : gender;
        details.Berth = berth === "" ? berth : "Any";
        if (details.PassName !== "") {
          reserved.push(details);
        }
        passCount++;
      }
      let calcFare: any = 0;
      // tslint:disable-next-line: forin
      for (const j in this.cities) {
        if (this.startPoint.value === this.cities[j].name) {
          calcFare = calcFare + this.cities[j].fare;
        }
        if (this.endPoint.value === this.cities[j].name) {
          calcFare = calcFare + this.cities[j].fare;
        }
      }
      const displayAmt: any = document.getElementById("amount");
      if (this.ticketType.value === "Economy Class" && displayAmt) {
        displayAmt.innerText =
          "Total payable amount: $" + passCount * (300 + calcFare);
      } else if (this.ticketType.value === "Business Class" && displayAmt) {
        displayAmt.innerText =
          "Total payable amount: $" + passCount * (500 + calcFare);
      } else if (this.ticketType.value === "Common Class" && displayAmt) {
        displayAmt.innerText =
          "Total payable amount: $" + passCount * (150 + calcFare);
      }
    }
    setTimeout(() => {
      (this.ticketDetailGrid || []).dataSource = reserved;
      this.ticketDetailGrid.dataBind();
    }, 100);
  }

  public content0() {
    return (
      <div id="booking">
        <div className="wizard-title">Plan your journey</div>
        <div className="responsive-align">
          <div className="row">
            <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6 search-item">
              <DropDownListComponent
                ref={dropdownlist => {
                  this.startPoint = dropdownlist!;
                }}
                width="100%"
                dataSource={this.cities}
                fields={this.autoCompleteFields}
                placeholder="From"
                floatLabelType="Auto"
              />
            </div>
            <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6 search-item">
              <DropDownListComponent
                ref={dropdownlist => {
                  this.endPoint = dropdownlist!;
                }}
                width="100%"
                dataSource={this.cities}
                fields={this.autoCompleteFields}
                placeholder="To"
                floatLabelType="Auto"
              />
            </div>
          </div>
          <div className="row">
            <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6 search-item">
              <DatePickerComponent
                ref={calendar => (this.journeyDate = calendar!)}
                width="100%"
                placeholder="Journey Date"
                floatLabelType="Auto"
                min={this.dateMin}
                max={this.dateMax}
                focus={this.focusIn}
              />
            </div>
            <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6 search-item">
              <DropDownListComponent
                ref={dropdownlist => (this.ticketType = dropdownlist!)}
                dataSource={this.quotas}
                placeholder="Ticket type"
                floatLabelType="Auto"
                fields={this.fields}
              />
            </div>
          </div>
          <div className="btn-container">
            <button
              id="searchNext"
              className="e-btn"
              onClick={this.btnClicked.bind(this)}
            >
              Search Train
            </button>
          </div>
          <span id="err1" />
        </div>
      </div>
    );
  }

  public content1() {
    return (
      <div id="selectTrain">
        <div className="wizard-title">Select the train from the list </div>
        <GridComponent
          ref={grid => (this.availTrainGrid = grid!)}
          width="100%"
          rowSelected={this.trainSelected.bind(this)}
        >
          <ColumnsDirective>
            <ColumnDirective
              field="TrainNo"
              headerText="Train No"
              width={120}
              type="number"
            />
            <ColumnDirective field="Name" headerText="Name" width={140} />
            <ColumnDirective
              field="Departure"
              headerText="Departure"
              width={120}
            />
            <ColumnDirective field="Arrival" headerText="Arrival" width={140} />
            <ColumnDirective
              field="Availability"
              headerText="Availability"
              width={140}
              type="number"
            />
          </ColumnsDirective>
        </GridComponent>
        <br />
        <div className="btn-container">
          <button
            id="goToSearch"
            className="e-btn"
            onClick={this.btnClicked.bind(this)}
          >
            Back
          </button>
          <button
            id="bookTickets"
            className="e-btn"
            onClick={this.btnClicked.bind(this)}
          >
            Continue
          </button>
        </div>
        <span id="err2" />
      </div>
    );
  }

  public content2() {
    return (
      <div id="details">
        <div className="details-page wizard-title">
          Enter the passenger details
        </div>
        <div id="PassengersList">
          <table id="passenger-table">
            <colgroup>
              <col />
              <col />
              <col />
              <col />
              <col />
              <col />
            </colgroup>
            <thead>
              <tr>
                <th className="name-header">Name</th>
                <th className="age-header">Age</th>
                <th className="gender-header">Gender</th>
                <th className="type-header">Berth Preference</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>
                  <input
                    className="e-input"
                    id="pass_name1"
                    type="text"
                    placeholder="Passenger Name"
                  />
                </td>
                <td>
                  <NumericTextBoxComponent
                    ref={numerictextbox => {
                      this.pass_age1 = numerictextbox!;
                    }}
                    showSpinButton={false}
                    min={1}
                    max={100}
                    value={18}
                    format="n0"
                  />
                </td>
                <td>
                  <DropDownListComponent
                    ref={dropdownlist => {
                      this.pass_gender1 = dropdownlist!;
                    }}
                    dataSource={this.gender}
                    text="Male"
                    fields={this.fields}
                  />
                </td>
                <td>
                  <DropDownListComponent
                    ref={dropdownlist => {
                      this.pass_berth1 = dropdownlist!;
                    }}
                    dataSource={this.berths}
                    placeholder="Optional"
                    fields={this.fields}
                  />
                </td>
              </tr>
              <tr>
                <td>
                  <input
                    id="pass_name2"
                    className="e-input"
                    type="text"
                    placeholder="Passenger Name"
                  />
                </td>
                <td>
                  <NumericTextBoxComponent
                    showSpinButton={false}
                    min={1}
                    max={100}
                    value={18}
                    format="n0"
                  />
                </td>
                <td>
                  <DropDownListComponent
                    ref={dropdownlist => {
                      this.pass_gender2 = dropdownlist;
                    }}
                    dataSource={this.gender}
                    text="Male"
                    fields={this.fields}
                  />
                </td>
                <td>
                  <DropDownListComponent
                    ref={dropdownlist => {
                      this.pass_berth2 = dropdownlist;
                    }}
                    dataSource={this.berths}
                    placeholder="Optional"
                    fields={this.fields}
                  />
                </td>
              </tr>
              <tr>
                <td>
                  <input
                    id="pass_name3"
                    className="e-input"
                    type="text"
                    placeholder="Passenger Name"
                  />
                </td>
                <td>
                  <NumericTextBoxComponent
                    showSpinButton={false}
                    min={1}
                    max={100}
                    value={18}
                    format="n0"
                  />
                </td>
                <td>
                  <DropDownListComponent
                    ref={dropdownlist => {
                      this.pass_gender3 = dropdownlist;
                    }}
                    dataSource={this.gender}
                    text="Male"
                    fields={this.fields}
                  />
                </td>
                <td>
                  <DropDownListComponent
                    ref={dropdownlist => {
                      this.pass_berth3 = dropdownlist;
                    }}
                    dataSource={this.berths}
                    placeholder="Optional"
                    fields={this.fields}
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <br />
        <div className="btn-container">
          <button
            id="goBackToBook"
            className="e-btn"
            onClick={this.btnClicked.bind(this)}
          >
            Back
          </button>
          <button
            id="confirmTickets"
            className="e-btn"
            onClick={this.btnClicked.bind(this)}
          >
            Continue
          </button>
        </div>
        <span id="err3" />
      </div>
    );
  }

  public content3() {
    return (
      <div id="confirm">
        <div className="tab-title1 wizard-title">
          Confirm the details and proceed
        </div>
        <GridComponent
          ref={grid => (this.ticketDetailGrid = grid)}
          width="100%"
        >
          <ColumnsDirective>
            <ColumnDirective
              field="TrainNo"
              headerText="Train No"
              width={120}
              type="number"
            />
            <ColumnDirective field="PassName" headerText="Name" width={140} />
            <ColumnDirective field="Gender" headerText="Gender" width={120} />
            <ColumnDirective field="Berth" headerText="Berth" width={140} />
          </ColumnsDirective>
        </GridComponent>
        <br />
        <div id="amount" />
        <br />
        <div className="btn-container">
          <button
            id="goBackDetails"
            className="e-btn"
            onClick={this.btnClicked.bind(this)}
          >
            Back
          </button>
          <button
            id="makePayment"
            className="e-btn"
            onClick={this.btnClicked.bind(this)}
          >
            Pay
          </button>
        </div>
      </div>
    );
  }

  public render() {
    return (
      <div>
        <div className="col-lg-12 control-section e-tab-section">
          <div className="e-sample-resize-container">
            <TabComponent
              id="tab-wizard"
              ref={tab => (this.tab = tab!)}
              heightAdjustMode="None"
              height={390}
              selecting={this.tabSelected.bind(this)}
            >
              <TabItemsDirective>
                <TabItemDirective
                  header={this.headerText[0]}
                  content={this.content0.bind(this)}
                />
                <TabItemDirective
                  header={this.headerText[1]}
                  content={this.content1.bind(this)}
                  disabled={true}
                />
                <TabItemDirective
                  header={this.headerText[2]}
                  content={this.content2.bind(this)}
                  disabled={true}
                />
                <TabItemDirective
                  header={this.headerText[3]}
                  content={this.content3.bind(this)}
                  disabled={true}
                />
              </TabItemsDirective>
            </TabComponent>
            <DialogComponent
              ref={dialog => (this.alertDlg = dialog!)}
              header="Success"
              width={250}
              isModal={true}
              visible={false}
              showCloseIcon={true}
              content="Your payment successfully processed"
              target={this.dlgTarget}
              buttons={this.dlgButtons}
              created={this.dlgCreated.bind(this)}
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
