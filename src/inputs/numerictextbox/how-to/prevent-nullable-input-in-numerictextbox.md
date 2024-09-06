# Prevent nullable input in NumericTextBox

By default, the value of the NumericTextBox sets to null. In some applications, the value of the NumericTextBox should not be null at any instance. In such cases, following sample can be used to prevent nullable input in NumericTextBox.

{% tab template="numeric-textbox/nullable-input", isDefaultActive = "true", sourceFiles="app/**/*.tsx,styles.css" %}

```typescript
import { NumericBlurEventArgs, NumericTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public numericInstance: any;
  public numericValue: number = 0;
  constructor(props: any) {
    super(props);
    this.onCreate = this.onCreate.bind(this);
    this.onBlur = this.onBlur.bind(this);
  }

  // prevents nullable value during initialization
  public onCreate() {
        if (this.numericInstance.value == null) {
              this.numericInstance.value = 0;
              this.numericInstance.dataBind()
        }
  }
  public onBlur(args: NumericBlurEventArgs) {
        if (args.value == null) {
            this.numericInstance.value = 0;
            this.numericInstance.dataBind()
        }
    }
  public render() {
    return (
      <NumericTextBoxComponent id="numeric" value={this.numericValue} ref={(numeric) => { this.numericInstance = numeric as NumericTextBoxComponent; }} created={this.onCreate} blur={this.onBlur} />
    );
  }
}
ReactDOM.render(<App />, document.getElementById('numeric1'));

 ```

{% endtab %}
