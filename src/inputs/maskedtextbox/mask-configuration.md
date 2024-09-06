---
title: "Mask Configuration"
component: "MaskedTextBox"
description: "Different mask configuration in masked textbox"
---

# Mask Configuration

The mask is a combination of standard and custom mask elements, that validates the user input based on its behavior.

> When the mask value is empty, the MaskedTextBox behaves as an input element with text type.

## Standard mask elements

The following table shows the list of mask elements and its behavior based on
 [MSDN](https://msdn.microsoft.com/en-us/library/system.windows.forms.maskedtextbox.mask.aspx) standard.

The mask can be formed by combining any one or more of these mask elements.

| Mask Element | Description |
| ------------- | ------------- |
| 0 | Digit required. This element will accept any single digit from **0** to **9**. |
| 9 | Digit or space, optional. |
| # | Digit or space, optional, Plus(**+**) and minus(**-**) signs are allowed. |
| L | Letter required. It will accept letters **a-z** and **A-Z**. |
| ? | Letter or space, optional. |
| & | Requires a character. |
| C | Character or space, optional. |
| A | Alphanumeric **(A-Za-z0-9)** required.|
| a | Alphanumeric **(A-Za-z0-9)** or space, optional. |
| < | Shift down. Converts all characters to lower case. |
| > | Shift up. Converts all characters to upper case. |
| &#124; | Disable a previous shift up or shift down. |
| \\\\ | Escapes a mask character, turning it into a literal. |
| All other characters | Literals. All non-mask elements (literals) will appear as themselves within MaskedTextBox. |

The following example demonstrates the usage of standard mask elements.

{% tab template="masked-textbox/standard-masks", sourceFiles="app/**/*.tsx" %}

```typescript
import { MaskedTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

// sets mask with the mask element '#' which accepts any single digit from '0' to '9',
// space, + and - signs
ReactDOM.render(<MaskedTextBoxComponent mask={'#####'}  placeholder= {'Mask ##### (ex: 012+-)'} floatLabelType='Always'/>
,document.getElementById('mask1'));

// sets mask format with the mask element 'L' which allows only alphabets('A-Z and a-z')
ReactDOM.render(<MaskedTextBoxComponent mask={'LLLLLL'}  placeholder= {'Mask LLLLLL (ex: Sample)'} floatLabelType='Always'/>
,document.getElementById('mask2'));

// sets mask format with the mask element '&' which allows `alphabets`, `numbers`
// and `special characters`
ReactDOM.render(<MaskedTextBoxComponent mask={'&&&&&'}  placeholder= {'Mask &&&&& (ex: A12@#)'} floatLabelType='Always'/>
,document.getElementById('mask3'));

// sets mask format with the mask element `>` which converts all characters that follow
// to upper case and `<` which converts all characters that follow to lower case
ReactDOM.render(<MaskedTextBoxComponent mask={'>LLL<LLL'}  placeholder= {'Mask >LLL<LL (ex: SAMple)'} floatLabelType='Always'/>
,document.getElementById('mask4'));

// sets mask format with the mask element '\\' which turns mask element `A` into
// a literal and it displays the alphabet `A`
ReactDOM.render(<MaskedTextBoxComponent mask={'\\A999'}  placeholder= {'Mask \\A999 (ex: A321)'} floatLabelType='Always'/>
,document.getElementById('mask5'));

```

{% endtab %}

## Custom mask elements

Other than the above standard mask elements, the mask can be configured with the custom characters or regular expression to define a custom behavior.

### Custom characters

You can define any of the non-mask element as the mask element
and its behavior through the [`customCharacters`](../api/maskedtextbox#customcharacters) property.

In the following example, non-mask element `P` accepts the values `P, A, p, a` and `M` accepts the values `M, m`
 as mentioned in the custom characters collection.

{% tab template="masked-textbox/getting-started", sourceFiles="app/**/*.tsx" %}

```typescript
import { MaskedTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

export default class App extends React.Component<{}, {}> {
  public chars: any = { P: 'P,A,a,p', M: 'M,m'};
  public render() {
    return (
        // sets custom characters collection for non-mask elements 'P' and 'M'
        <MaskedTextBoxComponent mask='00:00 >PM'  customCharacters= {this.chars}  placeholder= 'Time (ex: 10:00 PM, 10:00 AM)' floatLabelType='Always'/>
    );
  }
}

ReactDOM.render(<App />, document.getElementById('maskedContainer'));

```

{% endtab %}

### Regular expression

Instead of the mask element, you can define your own regular expression to validate the input of a particular input place.
The regular expressions should be wrapped by the square brackets (e.g.,: [`Regex`]).

In the following example, regular expression has been set for each input places.

{% tab template="masked-textbox/regularExpression", sourceFiles="app/**/*.tsx" %}

```typescript
import { MaskedTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(<MaskedTextBoxComponent mask='[0-2][0-9][0-9].[0-2][0-9][0-9].[0-2][0-9][0-9].[0-2][0-9][0-9]' placeholder= 'IP Address (ex: 212.212.111.222)' floatLabelType='Always' />
,document.getElementById('masktextbox'));

 ```

{% endtab %}

## Prompt character

The Prompt character is a prompting symbol in the MaskedTextBox for the mask elements. The symbol is used to show the input positions in the MaskedTextBox. You can customize the prompt character of MaskedTextBox
by using the [`promptChar`](../api/maskedtextbox#promptchar) property.

The following example demonstrates the MaskedTextBox with customized prompt character as `*`.

{% tab template="masked-textbox/getting-started", sourceFiles="app/**/*.tsx" %}

```typescript

import { MaskedTextBoxComponent } from '@syncfusion/ej2-react-inputs';
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(<MaskedTextBoxComponent mask={'999-999-9999'} promptChar={'#'} /> ,document.getElementById('maskedContainer'));

```

{% endtab %}
