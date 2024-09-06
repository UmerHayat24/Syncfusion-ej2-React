---
title: "Create wizard using Accordion"
component: "Accordion"
description: "This online shopping example demonstrates how to create multiple components inside the Essential JS 2 Accordion control."
---

# Create wizard using Accordion

Accordion items can be disabled dynamically by passing the index and boolean value with the ['enableItem'](../../api/accordion#enableitem) method and also dynamically expand the item using [`expandItem`](../../api/accordion#expanditem) method.

The below Wizard sample is designed for Online Shopping model. In this,  each Accordion item is integrated with required components to fill
the details and designed for getting user details and making payment at the end. Each field is provided with validation for all mandatory
option to enable/disable to next Accordion.  In below sample, accordion items can be disabled dynamically with [`enableItem`](../../api/accordion#enableitem) method using [`created`](../../api/accordion#created) event.

{% tab template="accordion/accordion-disable", compileJsx=true %}

```typescript

import * as React from "react";
import * as ReactDOM from "react-dom";

import { enableRipple } from '@syncfusion/ej2-base';
import { DialogComponent } from '@syncfusion/ej2-react-popups';
import { DatePickerComponent } from '@syncfusion/ej2-react-calendars';
import { NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import { AccordionComponent, AccordionItemsDirective, AccordionItemDirective } from '@syncfusion/ej2-react-navigations';

export class ReactApp extends React.Component<{}, {}> {
  public success: string = "Your payment successfully processed";
  public email_alert: string = "Enter valid email address";
  public mobile_alert: string = "Mobile number length should be 10";
  public card_alert: string = "Card number length should be 16";
  public cvv_alert: string = "CVV number length should be 3";
  public dlgTarget: HTMLElement = document.body;

  public dlgButtons: Object[] = [
    {
      buttonModel: { content: "Ok", isPrimary: true },
      click: () => {
        this.alertDlg.hide();
        if (
          this.accordion.expandedItems[0] === 2 &&
          this.alertDlg.content === this.success
        ) {
          this.accordion.enableItem(0, true);
          this.accordion.enableItem(1, false);
          this.accordion.enableItem(2, false);
          this.accordion.expandItem(true, 0);
        }
      }
    }
  ];

  public dlgCreated(): void {
    this.hide();
  }

  public acrdnCreated(): void {
    this.enableItem(1, false);
    this.enableItem(2, false);
  }

  public btnClick(e): void {
    switch (e.target.id) {
      case "Continue_Btn":
        let email: string = document.getElementById("email");
        let password: string = document.getElementById("password");
        if (email.value !== "" && password.value !== "") {
          if (this.checkMail(email.value)) {
            email.value = password.value = "";
            this.accordion.enableItem(1, true);
            this.accordion.enableItem(0, false);
            this.accordion.expandItem(true, 1);
          }
          document.getElementById("err1").classList.remove("show");
        } else {
          document.getElementById("err1").classList.add("show");
        }
        break;
      case "Continue_BtnAdr":
        let name: string = document.getElementById("name");
        let address: string = document.getElementById("address");
        if (
          name.value !== "" &&
          address.value !== "" &&
          this.mobile.value != null
        ) {
          if (this.checkMobile(this.mobile.value)) {
            this.accordion.enableItem(2, true);
            this.accordion.enableItem(1, false);
            this.accordion.expandItem(true, 2);
          }
          document.getElementById("err2").classList.remove("show");
        } else {
          document.getElementById("err2").classList.add("show");
        }
        break;
      case "Back_Btn":
        this.accordion.enableItem(1, true);
        this.accordion.enableItem(2, false);
        this.accordion.expandItem(true, 1);
        break;
      case "Save_Btn":
        let cardHolder: string = document.getElementById("cardHolder");
        if (
          this.cardNo.value != null &&
          cardHolder.value !== "" &&
          this.expiry.value != null &&
          this.cvv.value != null
        ) {
          if (this.checkCardNo(this.cardNo.value)) {
            if (this.checkCVV(this.cvv.value)) {
              this.alertDlg.content = this.success;
              this.alertDlg.show();
            }
          }
          document.getElementById("err3").classList.remove("show");
        } else {
          document.getElementById("err3").classList.add("show");
        }
        break;
    }
  }

  public checkMail(mail: string): void {
    if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(mail)) {
      return true;
    } else {
      this.alertDlg.content = this.email_alert;
      this.alertDlg.show();
      return false;
    }
  }

  public checkMobile(mobile: number): void {
    if (/^\d{10}$/.test(mobile)) {
      return true;
    } else {
      this.alertDlg.content = this.mobile_alert;
      this.alertDlg.show();
      return false;
    }
  }

  public checkCardNo(cardNo: number): void {
    if (/^\d{16}$/.test(cardNo)) {
      return true;
    } else {
      this.alertDlg.content = this.card_alert;
      this.alertDlg.show();
      return false;
    }
  }

  public checkCVV(cvv: number): void {
    if (/^\d{3}$/.test(cvv)) {
      return true;
    } else {
      this.alertDlg.content = this.cvv_alert;
      this.alertDlg.show();
      return false;
    }
  }
  public content0() {
    const alignCenter = { textAlign: 'center' };
    return (
      <div id="Sign_In_Form">
        <form id="formId">
          <div className="form-group">
            <div className="e-float-input">
              <input type="text" id="email" name="Email" required />
              <span className="e-float-line" />
              <label className="e-float-text">Email</label>
            </div>
            <div className="e-float-input">
              <input id="password" type="password" name="Password" required />
              <span className="e-float-line" />
              <label className="e-float-text" for="password">
                Password
              </label>
            </div>
          </div>
        </form>
        <div style={alignCenter}>
          <button
            className="e-btn"
            id="Continue_Btn"
            onClick={this.btnClick.bind(this)}
          >
            Continue
          </button>
          <div id="err1">* Please fill all fields</div>
        </div>
      </div>
    );
  }
  public content1() {
    const alignCenter = { textAlign: 'center' };
    return (
      <div id="Address_Fill">
        <form id="formId_Address">
          <div className="form-group">
            <div className="e-float-input">
              <input type="text" id="name" name="Name" required />
              <span className="e-float-line" />
              <label className="e-float-text" for="name">
                Name
              </label>
            </div>
          </div>
          <div className="form-group">
            <div className="e-float-input">
              <input type="text" id="address" name="Address" required />
              <span className="e-float-line" />
              <label className="e-float-text" for="address">
                Address
              </label>
            </div>
          </div>
          <div className="form-group">
            <NumericTextBoxComponent
              ref={numerictextbox => {
                this.mobile = numerictextbox;
              }}
              format="0"
              placeholder="Mobile"
              floatLabelType="Auto"
              showSpinButton={false}
            />
          </div>
        </form>
        <div style={alignCenter}>
          <button
            className="e-btn"
            id="Continue_BtnAdr"
            onClick={this.btnClick.bind(this)}
          >
            Continue
          </button>
          <div id="err2">* Please fill all fields</div>
        </div>
      </div>
    );
  }
  public content2() {
    const alignCenter = { textAlign: 'center' };
    return (
      <div id="Card_Fill">
        <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
          <div className="form-group">
            <NumericTextBoxComponent
              ref={numerictextbox => {
                this.cardNo = numerictextbox;
              }}
              format="0"
              placeholder="Card No"
              floatLabelType="Auto"
              showSpinButton={false}
            />
          </div>
        </div>
        <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
          <div className="form-group">
            <div className="e-float-input">
              <input type="text" id="cardHolder" name="cardHolder" required />
              <span className="e-float-line" />
              <label className="e-float-text" for="cardHolder">
                CardHolder Name
              </label>
            </div>
          </div>
        </div>
        <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
          <DatePickerComponent
            ref={calendar => (this.expiry = calendar)}
            width="100%"
            format="MM/yyyy"
            placeholder="Expiry Date"
            floatLabelType="Auto"
          />
        </div>
        <div className="col-xs-6 col-sm-6 col-lg-6 col-md-6">
          <div className="form-group">
            <NumericTextBoxComponent
              ref={numerictextbox => {
                this.cvv = numerictextbox;
              }}
              format="0"
              placeholder="CVV"
              floatLabelType="Auto"
              showSpinButton={false}
            />
          </div>
        </div>
        <div style={alignCenter}>
          <button
            className="e-btn"
            id="Back_Btn"
            onClick={this.btnClick.bind(this)}
          >
            Back
          </button>
          <button
            className="e-btn"
            id="Save_Btn"
            onClick={this.btnClick.bind(this)}
          >
            Save
          </button>
          <div id="err3">* Please fill all fields</div>
        </div>
      </div>
    );
  }
  render() {
    return (
      <div>
        <div className="template_title"> Online Shopping Payment Module</div>

        <DialogComponent
          ref={dialog => (this.alertDlg = dialog)}
          header="Alert"
          width={200}
          isModal={true}
          content=""
          target={this.dlgTarget}
          buttons={this.dlgButtons}
          created={this.dlgCreated}
        />

        <AccordionComponent
          ref={accordion => (this.accordion = accordion)}
          created={this.acrdnCreated}
        >
          <AccordionItemsDirective>
            <AccordionItemDirective
              expanded={true}
              header="Sign In"
              content={this.content0.bind(this)}
            />
            <AccordionItemDirective
              header="Delivery Address"
              content={this.content1.bind(this)}
            />
            <AccordionItemDirective
              header="Card Details"
              content={this.content2.bind(this)}
            />
          </AccordionItemsDirective>
        </AccordionComponent>
      </div>
    );
  }
}
ReactDOM.render(<ReactApp />, document.getElementById("element"));

```

{% endtab %}
