# Integrate avatar into Badge

The badge is dependent and supportive component, and it can be used with avatar to create a notification avatar.
The default avatar (.`e-avatar`) and circle avatar (.`e-avatar-circle`) have been used with notification
badges (.`e-badge-notification`) in the following sample.

{% tab template="avatar/badge", isDefaultActive=true, sourceFiles="app/**/*.tsx,index.html,index.css" %}

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

class ReactApp extends React.Component<{}, {}> {
  render() {
       return (
        <div>
            <div className="sample_container avatar-badge">
                <div className="avatar-block">
                    {/* Card Component  */}
                    <div className="e-card e-avatar-showcase">
                        <div className="e-card-content">
                            <div className="avatar-sub-block">
                                {/* xSmall Avatar */}
                                <div className="e-avatar e-avatar-xsmall">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification e-badge-circle">6</span>
                            </div>
                            <div className="avatar-sub-block">
                                {/* Small Avatar */}
                                <div className="e-avatar e-avatar-small">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification e-badge-circle">12</span>
                            </div>
                            <div className="avatar-sub-block">
                                {/* Avatar */}
                                <div className="e-avatar">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification">46</span>
                            </div>
                            <div className="avatar-sub-block">
                                {/* Large Avatar */}
                                <div className="e-avatar e-avatar-large">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification">82</span>
                            </div>
                            <div className="avatar-sub-block">
                                {/* xLarge Avatar */}
                                <div className="e-avatar e-avatar-xlarge">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification">99+</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div className="circleAvatar avatar-block">
                    {/* Card Component  */}
                    <div className="e-card e-avatar-showcase">
                        <div className="e-card-content">
                            <div className="avatar-sub-block">
                                {/* xSmall Circle Avatar */}
                                <div className="e-avatar e-avatar-circle e-avatar-xsmall">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification e-badge-circle">6</span>
                            </div>
                            <div className="avatar-sub-block">
                                {/* Small Circle Avatar */}
                                <div className="e-avatar e-avatar-circle e-avatar-small">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification e-badge-circle">12</span>
                            </div>
                            <div className="avatar-sub-block">
                                {/* Circle Avatar */}
                                <div className="e-avatar e-avatar-circle">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification">46</span>
                            </div>
                            <div className="avatar-sub-block">
                                {/* Large Circle Avatar */}
                                <div className="e-avatar e-avatar-circle e-avatar-large">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification">82</span>
                            </div>
                            <div className="avatar-sub-block">
                                {/* xLarge Circle Avatar */}
                                <div className="e-avatar e-avatar-circle e-avatar-xlarge">
                                    <img src="https://ej2.syncfusion.com/demos/src/grid/images/2.png" alt="profile_pic" />
                                </div>
                                {/* Notification Badge  */}
                                <span className="e-badge e-badge-primary e-badge-overlap e-badge-notification">99+</span>
                            </div>
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
