---
title: "Find and Replace"
component: "DocumentEditor"
description: "Learn how to find a portion of text in React document editor and replace it with another portion of text."
---

# Find and Replace

The document editor component searches a portion of text in the document through a built-in interface called `OptionsPane` or rich APIs. When used in combination with selection performs various operations on the search results like replacing it with some other text, highlighting it, making it bolder, and more.

## Options pane

This provides the options to search for a portion of text in the document. After search operation is completed, the search results will be displayed in a list and options to navigate between them. The current occurrence of matched text or all occurrences with another text can be replaced by switching to `Replace` tab. This pane is opened using the keyboard shortcut `CTRL+F`. You can also open it programmatically using the following sample code.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, SfdtExport, Selection, Editor, BordersAndShadingDialog } from '@syncfusion/ej2-react-documenteditor';

//Inject require module.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, BordersAndShadingDialog);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        let sfdt: string = `{
            "sections": [
                {
                    "blocks": [
                        {
                            "inlines": [
                                {
                                    "characterFormat": {
                                        "bold": true,
                                        "italic": true
                                    },
                                    "text": "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base."
                                }
                            ]
                        }
                    ]
                }
            ]
        }`;
        //Open the document in Document Editor.
        this.documenteditor.open(sfdt);
    }

    showHideOptionsPane(): void {
        //Open options pane.
        this.documenteditor.showOptionsPane();
    }
    render() {
        return (
            <div>
                <button onClick={this.showHideOptionsPane.bind(this)}>OptionsPane</button>
                <DocumentEditorComponent id="container" height={'330px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSearch={true} enableOptionsPane={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

You can close the options pane by pressing `Esc` key.

## Search

The `Search` module of document editor exposes the following APIs:

|API Name|Type |Description|
|---|---|---|
|`findAll()` | Method |Searches for specified text in the whole document and highlights it with yellow.|
|`searchResults` |Property |This is an instance of `SearchResults`.|

Refer to the following code example.

```typescript
documenteditor.search.findAll('Some text', 'None');
```

## Search results

The `SearchResults` class provides information about the search results after a search operation is completed that can be identified using the `searchResultsChange` event. This will expose the following APIs:

|API Name|Type |Description|
|---|---|---|
|`length`|Property|Returns the total number of results found on the search.|
|`index`|Property|Returns the index of selected search result. You can change the value for this property to move the selection.|
|`replaceAll()`|Method|Replaces all the occurrences with specified text.|
|`clear()`|Method|Clears the search result.|

## SearchResultsChange event

`DocumentEditor` exposes the `searchResultsChange’`event that will be triggered whenever search results are changed. Consider the following scenarios:

* A search operation is completed with some results.
* The results are replaced with some other text, since it will be cleared automatically.
* The results are cleared explicitly.

Refer to the following code example.

```typescript
documenteditor.searchResultsChange = function() {

};
```

## Customize find and replace

Using the exposed APIs, you can customize the find and replace functionality in your application. Refer to the following sample code.

{% tab compileJsx=true%}

```typescript

import * as ReactDOM from 'react-dom';
import * as React from 'react';
import { DocumentEditorComponent, SfdtExport, Selection, Editor, Search } from '@syncfusion/ej2-react-documenteditor';

//Inject require module.
DocumentEditorComponent.Inject(SfdtExport, Selection, Editor, Search);
export class Default extends React.Component<{}, {}> {
    public documenteditor: DocumentEditorComponent;

    public componentDidMount(): void {
        let sfdt: string = `{
            "sections": [
                {
                    "blocks": [
                        {
                            "inlines": [
                                {
                                    "characterFormat": {
                                        "bold": true,
                                        "italic": true
                                    },
                                    "text": "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base."
                                }
                            ]
                        }
                    ]
                }
            ]
        }`;
        //Open the document in Document Editor.
        this.documenteditor.open(sfdt);
    }

    replaceAll(): void {
        let textToFind: string = (document.getElementById('find_text') as HTMLInputElement).value;
        let textToReplace: string = (document.getElementById('replace_text') as HTMLInputElement).value;
        if (textToFind !== '') {
            // Find all the occurences of given text
            this.documenteditor.searchModule.findAll(textToFind);
            if (this.documenteditor.searchModule.searchResults.length > 0) {
                // Replace all the occurences of given text
                this.documenteditor.searchModule.searchResults.replaceAll(textToReplace);
            }
        }
    }
    render() {
        return (
            <div>
                <button onClick={this.replaceAll.bind(this)}>Replace All</button>
                <DocumentEditorComponent id="container" height={'590px'} ref={(scope) => { this.documenteditor = scope; }} isReadOnly={false} enableSelection={true} enableEditor={true} enableSearch={true} />
            </div>
        );
    }
}
ReactDOM.render(<Default />, document.getElementById('sample'));

```

{% endtab %}

## See Also

* [Options pane](../document-editor/dialog#options-pane)
* [Feature modules](../document-editor/feature-module/)
