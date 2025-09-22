# Multi-Select DropDown

The multi-select dropdown is essentially a checkbox list that is displayed in a dropdown-like way. It is useful when you want to allow users to select from a checkbox list, but don't have the space to display the entire list

https://github.com/stadium-software/multi-select-dropdown/assets/2085324/dff8cb5a-bf6e-4028-a8b9-4e94b2745792

## Version
Current version 1.3.1

1.1 Simplified setup requirements; Enhanced script to detect invalid parameter values

1.2 Fixed requiredFieldValidator bug (JS & CSS)

1.3 Removed script input parameter (any checkboxlist with class 'multi-select-dropdown' is converted)

1.3.1 Upgraded readme to 6.12+; fixed border display bug; converted px to rem

1.4 Integrated CSS with script

## Application Setup
1. Check the *Enable Style Sheet* checkbox in the application properties

## Global Script Setup

1. Create a Global Script and call it "MultiSelectDropDown"
2. Drag a Javascript action into the script and paste the Javascript below unaltered into the action
```javascript
/* Stadium Script Version 1.4 https://github.com/stadium-software/multi-select-dropdown/ */
loadCSS();
let clists = document.querySelectorAll(".multi-select-dropdown");
for (let i = 0; i < clists.length; i++) {
    let clist = clists[i];
    clist.classList.add("stadium-multi-select-dropdown");
    let header = document.createElement("div");
    header.textContent = "Select";
    header.classList.add("stadium-multi-select-dropdown-header", "control-container");
    header.addEventListener("click", function (e) {
        e.target.closest(".check-box-list-container").classList.toggle("expand");
    });
    let clistItems = clist.querySelectorAll("div")[0];
    clistItems.classList.add("stadium-multi-select-checkboxlist");
    clistItems.before(header);
}
function loadCSS() {
    let moduleID = "stadium-multi-select-dropdown";
    if (!document.getElementById(moduleID)) {
        let cssMain = document.createElement("style");
        cssMain.id = moduleID;
        cssMain.type = "text/css";
        cssMain.textContent = `
/* CSS version 1.0 https: //github.com/stadium-software/multi-select-dropdown */
.check-box-list-container:has(.stadium-multi-select-checkboxlist) {
	border: 0.1rem solid var(--multi-select-container-border-color, var(--BUTTON-BORDER-COLOR));
	position: relative;
	background-color: var(--multi-select-background-color, var(--CHECK-BOX-LIST-CONTAINER-BACKGROUND-COLOR));

    &:after {
        top: 0;
        right: 0;
    }

    .stadium-multi-select-checkboxlist {
        display: none;
        position: absolute;
        z-index: 10;
        top: 3.3rem;
        left: -0.1rem;
        border: 0.1rem solid var(--multi-select-container-border-color, var(--BUTTON-BORDER-COLOR));
        > div {
            box-shadow: rgba(0, 0, 0, 0.07) 0 0.1rem 0.1rem, rgba(0, 0, 0, 0.07) 0 0.2rem 0.2rem, rgba(0, 0, 0, 0.07) 0 0.4rem 0.4rem, rgba(0, 0, 0, 0.07) 0 0.8rem 0.8rem, rgba(0, 0, 0, 0.07) 0 1.6rem 1.6rem;
            background-color: var(--multi-select-background-color, var(--CHECK-BOX-LIST-CONTAINER-BACKGROUND-COLOR));
        }
    }
    .stadium-multi-select-dropdown-header {
        display: block;
        cursor: pointer;
        user-select: none;
        padding: 0 2.6rem var(--multi-select-container-padding, 0.6rem) var(--multi-select-container-padding, 0.6rem);
    }
    .stadium-multi-select-dropdown-header:after {
        content: "\\00BB";
        position: absolute;
        padding-left: 0.4rem;
        font-size: 2.2rem;
        height: 2rem;
        width: 2rem;
        transform: rotate(90deg);
        transform-origin: 67% 76%;
        transition: transform .1s;
    }
}
.check-box-list-container.expand:has(.stadium-multi-select-checkboxlist) {
    .stadium-multi-select-checkboxlist {
        display: block;
    }
    .multi-select-dropdown-header:after {
        transform: rotate(270deg) translate(0.8rem,-0.3rem);
    }
}
html {
    min-height: 100%;
    font-size: 62.5%;
}        
        `;
        document.head.appendChild(cssMain);
    }
}
document.body.addEventListener("click", function (e) {
    if (!e.target.closest(".check-box-list-container")) {
        let allDD = document.querySelectorAll(".check-box-list-container:has(.stadium-multi-select-checkboxlist)");
        for (let i = 0; i < allDD.length; i++) {
            allDD[i].classList.remove("expand");
        }
    }
});
```
## Multi-Select-DropDown
1. Drag a *CheckboxList* control onto a page and call it "MultiSelectDropDownCheckBoxList"
2. Add a class to the classes property of the "MultiSelectDropDownCheckBoxList" control to uniquely identiy the *CheckBoxList* on this page (e.g. "multi-select-checkboxlist")
3. Paste the example array below into the *Options* property of the "MultiSelectDropDownCheckBoxList" control to create some sample items (you can populate the checkbox list from any datasource)
```json
[
    {"text":"Item1","value":"Item1"},
    {"text":"Item2","value":"Item2"},
    {"text":"Item3","value":"Item3"},
    {"text":"Item4","value":"Item4"}
]
```

## Page.Load Setup
1. Drag the "MultiSelectDropDown" global script into the load event handler

## CSS
Variables exposed in the [*multi-select-variables.css*](multi-select-variables.css) file can be [customised](#customising-css).

### Customising CSS
1. Open the CSS file called [*multi-select-variables.css*](multi-select-variables.css) from this repo
2. Adjust the variables in the *:root* element as you see fit
3. Stadium 6.12+ users can comment out any variable they do **not** want to customise
4. Add the [*multi-select-variables.css*](multi-select-variables.css) to the "CSS" folder in the EmbeddedFiles (overwrite)
5. Paste the link tag below into the *head* property of your application (if you don't already have it there)
```html
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/multi-select-variables.css">
``` 
6. Add the file to the "CSS" inside of your Embedded Files in your application

## Upgrading Stadium Repos
Stadium Repos are not static. They change as additional features are added and bugs are fixed. Using the right method to work with Stadium Repos allows for upgrading them in a controlled manner. 

How to use and update application repos is described here: [Working with Stadium Repos](https://github.com/stadium-software/samples-upgrading)