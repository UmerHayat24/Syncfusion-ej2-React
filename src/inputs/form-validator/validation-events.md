# Validation Events

Validation events have two types of events. These are

* validationBegin
* validationComplete

## Validation Begin

`validationBegin` event triggers before the validation starts and also it invoke for each rules in validation process. Please find the below code snippet.

```typescript

validationBegin: function(args) {
        // ("Validation begin");
      },
```

The following values are passed in `args`. You can use this values in event validation.

| Fields  | Description |
|---------|-------------|
|`element`| Specifies the input element |
|`name`   | Specifies the event name (validationBegin)  |
|`param`  | Specifies the param value (true/false)  |
|`value`  | Specifies the input value  |

## Validation Complete

`validationComplete` event triggered after validation is completed and also it invoke  for each rules in validation process. Please find the below code snippet.

```typescript

validationComplete: function(args) {
        // ("Validation complete");
      }
```

The following values are passed in `args`. You can use this values in event validation.

| Fields  | Description |
|---------|-------------|
|`element`| Specifies the input element |
|`name`   | Specifies the event name (validationComplete)  |
|`param`  | Specifies the param value (true/false)  |
|`value`  | Specifies the input value  |
|`status` | Specifies the status (success/failure) |
|`inputName` | Specifies the type of input  |

Please find the simple sample for validation events.

{% tab template="form-validator/validation-events", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css", iframeHeight="600px" %}

```typescript
import { enableRipple } from '@syncfusion/ej2-base';
import { FormEventArgs, FormValidator, FormValidatorModel, ValidArgs } from '@syncfusion/ej2-inputs';
import { TimePickerComponent } from '@syncfusion/ej2-react-calendars';
import * as React from "react";
import * as ReactDOM from "react-dom";

// enable ripple effect
enableRipple(true);

export default class App extends React.Component<{}, {}> {
  public componentDidMount(): void {
        // add the rules for validation
         const options: FormValidatorModel = {
            // validation begin event
            validationBegin: (args: ValidArgs) => {
              const span = document.createElement("span");
              span.innerHTML = "Validation begin <hr>";
              const log = document.getElementById("EventLog") as HTMLElement;
              log.insertBefore(span, log.firstChild);
            },
            // validation complete event
            validationComplete: (args: FormEventArgs) => {
                if (args.status === "success") {
                  const span = document.createElement("span");
                  span.innerHTML = "Validation complete success <hr>";
                  const log = document.getElementById("EventLog") as HTMLElement;
                  log.insertBefore(span, log.firstChild);
                } else {
                  const span = document.createElement("span");
                  span.innerHTML = "Validation complete failure <hr>";
                  const log = document.getElementById("EventLog") as HTMLElement;
                  log.insertBefore(span, log.firstChild);
                }
            },  
        };
        // initialize the form validator
        const formObject: FormValidator = new FormValidator('#form1', options);
        formObject.addRules('timepicker', {required: true});
        (document.getElementById('clear') as HTMLElement).addEventListener('click', () => {
            (document.getElementById("EventLog") as HTMLElement).innerHTML = "";
        });  
    }

    public render() {
        return(
            <div>
            <div id='sample'>
                <form id='form1' method="post">
                    <div className='content-wrapper'>
                        <TimePickerComponent id="timepicker" placeholder="Select a Time"/>
                    </div>
                    <label className='e-error' id='timepickerError' htmlFor='timepicker'/>
                </form>
            </div>
            <div id="list_event">
            <h4><b>Event Trace</b></h4>
            <div id="evt">
                <div className="eventarea" >
                    {/*Event log element */}
                    <span className="EventLog" id="EventLog"/>
                </div>
                <div className="evtbtn">
                    {/*clear button element */}
                    <button className='e-btn' id="clear"> Clear </button>
                </div>
            </div>
        </div>
        </div>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('form-element'));
```

{% endtab %}
