# Show slider from hidden state

This section demonstrates how-to render the Slider component in hidden state and make it visible in button click. We can initialize Slider in hidden state by setting the display as none.

In the sample, by clicking on the button, we can make the Slider visible from hidden state, and we must also call the [`refresh`](https://ej2.syncfusion.com/javascript/documentation/api/base/component/#refresh) method of the Slider to render it properly based on its original dimensions.

{% tab template="slider/hidden-slider", isDefaultActive = "true", sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from 'react';
import * as ReactDOM from "react-dom";
import { SliderComponent, TicksDataModel, TooltipDataModel, SliderTickEventArgs, SliderTooltipEventArgs } from '@syncfusion/ej2-react-inputs';

export default class App extends React.Component<{}, {}> {
  public sliderInstance: SliderComponent;
  public min = new Date(2013, 6, 13, 11).getTime();
  public max = new Date(2013, 6, 13, 17).getTime();
  public value = new Date(2013, 6, 13, 13).getTime();
  public step = 3600000;
  public showButtons = true;

  // Slider ticks customization
  public ticks: TicksDataModel = { placement: "After", largeStep: 2 * 3600000 };
  public tooltip: TooltipDataModel = { placement: "Before", isVisible: true };

  renderingTicksHandler(args: SliderTickEventArgs) {
    let totalMiliSeconds = Number(args.value);
    let custom = { hour: "2-digit", minute: "2-digit" };
    args.text = new Date(totalMiliSeconds).toLocaleTimeString("en-us", custom);
  }

  tooltipChangeHandler(args: SliderTooltipEventArgs) {
    let totalMiliSeconds = Number(args.text);
    let custom = { hour: "2-digit", minute: "2-digit" };
    args.text = new Date(totalMiliSeconds).toLocaleTimeString("en-us", custom);
  }
  
  onClick(){
    const slider = document.getElementById("case");
    if(slider){
        slider.style.display = "block";
        this.sliderInstance.refresh();
    }
  }

  render() {
    return (
      <div id="container">
      <button onClick={this.onClick.bind(this)}>Button</button>
        <div id="case" className="wrap">
          <SliderComponent
            ref={t=>(this.sliderInstance = t as SliderComponent)}
            min={this.min}
            max={this.max}
            value={this.value}
            step={this.step}
            tooltip={this.tooltip}
            ticks={this.ticks}
            showButtons={true}
            tooltipChange={this.tooltipChangeHandler.bind(this) as any}
            renderingTicks={this.renderingTicksHandler.bind(this) as any}
          />
        </div>
      </div>
    );
  }}

ReactDOM.render(<App />, document.getElementById('element'));

```

{% endtab %}
