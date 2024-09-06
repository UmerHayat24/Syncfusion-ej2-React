# Avatar customization

## Colour customization

The avatar comes with default background colour (grey). This can be easily customized to the desired colour by adding custom
class or directly selecting the avatar class from the CSS.

{% tab template="avatar/color", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <span className="e-avatar e-avatar-xlarge e-avatar-circle green">AJ</span>
            <span className="e-avatar e-avatar-xlarge e-avatar-circle violet">JK</span>
            <span className="e-avatar e-avatar-xlarge e-avatar-circle rose">EL</span>
            <span className="e-avatar e-avatar-xlarge e-avatar-circle blue">SR</span>
            <span className="e-avatar e-avatar-xlarge e-avatar-circle red">PD</span>
        </div>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

## Customize avatar sizes

Even though the avatar comes with five predefined sizes, sometimes it's not enough. So, the avatar is designed in such a way
that the width and height will be relative to font-size. By changing the `font-size` of the avatar element, you can change
the width and height automatically.

{% tab template="avatar/custom-size", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <span className="e-avatar e-avatar-xlarge"></span>
            <span className="e-avatar e-avatar-large"></span>
            <span className="e-avatar"></span>
            <span className="e-avatar e-avatar-small"></span>
            <span className="e-avatar e-avatar-xsmall"></span>
        </div>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

## Use various media in avatar

Avatars can be used with a wide variety of media formats like SVG, font-icons, images, letters, words, etc. Some of them are given below.

{% tab template="avatar/media-formats", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <div className="sample_container avatar-types">
                <div className="avatar-block">
                    {/* Card Component  */}
                    <div className="e-card e-avatar-showcase">
                        <div className="e-card-content">
                            {/* XLarge Circle Avatar Component  */}
                            <div className="e-avatar e-avatar-xlarge e-avatar-circle">
                                    <img className="image" src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="avatar" />
                                </div>
                        </div>
                        <div className="e-card-content">
                            <div>Image</div>
                        </div>
                    </div>
                </div>

                <div className="avatar-block">
                    {/* Card Component  */}
                    <div className="e-card e-avatar-showcase">
                        <div className="e-card-content">
                            {/* XLarge Circle Avatar Component  */}
                            <div className="e-avatar e-avatar-xlarge e-avatar-circle">
                                <div className="svg_icons chrome"></div>
                            </div>
                        </div>
                        <div className="e-card-content">
                            <div>SVG</div>
                        </div>
                    </div>
                </div>

                <div className="avatar-block">
                    {/* Card Component  */}
                    <div className="e-card e-avatar-showcase">
                        <div className="e-card-content">
                            {/* XLarge Circle Avatar Component  */}
                            <div className="e-avatar e-avatar-xlarge e-avatar-circle">GR</div>
                        </div>
                        <div className="e-card-content">
                            <div>Initial</div>
                        </div>
                    </div>
                </div>

                <div className="avatar-block">
                    {/* Card Component  */}
                    <div className="e-card e-avatar-showcase">
                        <div className="e-card-content">
                            {/* XLarge Circle Avatar Component  */}
                            <div className="e-avatar e-avatar-xlarge e-avatar-circle">
                                <div className="e-people icons"></div>
                            </div>
                        </div>
                        <div className="e-card-content">
                            <div>Font Icon</div>
                        </div>
                    </div>
                </div>

                <div className="avatar-block">
                    {/* Card Component  */}
                    <div className="e-card e-avatar-showcase">
                        <div className="e-card-content">
                            {/* XLarge Circle Avatar Component  */}
                            <div className="e-avatar e-avatar-xlarge e-avatar-circle">User</div>
                        </div>
                        <div className="e-card-content">
                            <div>Word</div>
                        </div>
                    </div>
                </div>

                <div className="avatar-block">
                    {/* Card Component  */}
                    <div className="e-card e-avatar-showcase">
                        <div className="e-card-content">
                            {/* XLarge Circle Avatar Component  */}
                            <div className="e-avatar e-avatar-xlarge e-avatar-circle custom">
                                <div className="e-people icons"></div>
                            </div>
                        </div>
                        <div className="e-card-content">
                            <div>Custom</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
       );
  }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}

## Dynamic avatar rendering from datasource

We can render avatar component dynamically from a data-source. In this sample we have rendered the avatar component
using a data-source which contains the image source in different sizes dynamically. This is applicable also for
data-source from the server or remote data or AJAX. We have also rendered the avatar using `CSS` property
`background-image` and using image tag.

{% tab template="avatar/react-avatar", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {

    render() {
        let dataSource: { [key: string]: string }[] = [
            { src: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', size: 'e-avatar-xsmall' },
            { src: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', size: 'e-avatar-small' },
            { src: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', size: 'e-avatar' },
            { src: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', size: 'e-avatar-large' },
            { src: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', size: 'e-avatar-xlarge' }
        ];

        return (
            <div className='control-pane'>
                <div className="sample_container avatar-badge">
                    <div className="avatar-block">
                        <div className="e-card e-avatar-showcase">
                            <div className="e-card-content">
                                {dataSource.map(function (item) {
                                    return (<div className={`e-avatar e-avatar-circle ${item.size}`} style={{ backgroundImage: `url(${item.src})` }}></div>)
                                })}
                            </div>
                            <div className="e-card-content">
                                <div>Using <code>background-image</code> property</div>
                            </div>
                        </div>
                    </div>

                    <div className="circleAvatar avatar-block">
                        <div className="e-card e-avatar-showcase">
                            <div className="e-card-content">
                                {dataSource.map(function (item) {
                                    return (<div className={`e-avatar e-avatar-circle ${item.size}`} >
                                        <img src={item.src} />
                                    </div>)
                                })}
                            </div>
                            <div className="e-card-content">
                                <div>Using <code>img</code> tag</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        );
    }
}
ReactDOM.render(<ReactApp/>, document.getElementById("element"));
```

{% endtab %}