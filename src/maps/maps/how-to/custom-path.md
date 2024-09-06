# Custom path Map

Maps control can be customized as the desired layout using the custom path map feature. Here, the Maps control has been showcased with normal geometry type shapes to represent the bus seat selection layout.

{% tab compileJsx=true%}

```tsx
import { seatData } from 'seat.ts';
import * as React from 'react';
import {
  MapsComponent, LayersDirective, LayerDirective,
  Inject, Selection
} from '@syncfusion/ej2-react-maps';
import * as ReactDOM from 'react-dom';

class App extends React.Component {
    render() {
        return (
          <div className='control-section row'>
            <div className='col-md-8'>
              <div style={{ width: 200, margin: 'auto', paddingBottom: 20 }}>
                <div id="sampletitle">Bus seat selection</div>
              </div>
              <div style={{ border: '3px solid darkgray', width: 200, display: 'block', margin: 'auto' }}>
                <MapsComponent id="element" height='400'>
                  <Inject services={[Selection]} />
                  <LayersDirective>
                    <LayerDirective shapeData={seat} geometryType='Normal'>
                    </LayerDirective>
                  </LayersDirective>
                </MapsComponent>
              </div></div></div>);
      }
}
ReactDOM.render(<App/>, document.getElementById('maps'));
```

{% endtab %}