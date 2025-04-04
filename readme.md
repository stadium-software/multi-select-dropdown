# Multi-Select DropDown

The multi-select dropdown is essentially a checkbox list that is displayed in a dropdown-like way. It is useful when you want to allow users to select from a checkbox list, but don't have the space to display the entire list

https://github.com/stadium-software/multi-select-dropdown/assets/2085324/dff8cb5a-bf6e-4028-a8b9-4e94b2745792

## Version
Current version 1.3.1

1.1 Simplified setup requirements; Enhanced script to detect invalid parameter values

1.2 Fixed requiredFieldValidator bug (JS & CSS)

1.3 Removed script input parameter (any checkboxlist with class 'multi-select-dropdown' is converted)

1.3.1 Upgraded readme to 6.12+; fixed border display bug; converted px to rem

## Application Setup
1. Check the *Enable Style Sheet* checkbox in the application properties

## Global Script Setup

1. Create a Global Script and call it "MultiSelectDropDown"
2. Drag a Javascript action into the script and paste the Javascript below unaltered into the action
```javascript
/* Stadium Script Version 1.3 https://github.com/stadium-software/multi-select-dropdown/ */
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
The CSS below is required for the correct functioning of the module. Variables exposed in the [*multi-select-variables.css*](multi-select-variables.css) file can be [customised](#customising-css).

### Before v6.12
1. Create a folder called "CSS" inside of your Embedded Files in your application
2. Drag the two CSS files from this repo [*multi-select-variables.css*](multi-select-variables.css) and [*multi-select.css*](multi-select.css) into that folder
3. Paste the link tags below into the *head* property of your application
```html
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/multi-select.css">
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/multi-select-variables.css">
``` 

### v6.12+
1. Create a folder called "CSS" inside of your Embedded Files in your application
2. Drag the CSS files from this repo [*multi-select.css*](multi-select.css) into that folder
3. Paste the link tag below into the *head* property of your application
```html
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/multi-select.css">
``` 

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

**NOTE: Do not change any of the CSS in the 'multi-select.css' file**

## Upgrading Stadium Repos
Stadium Repos are not static. They change as additional features are added and bugs are fixed. Using the right method to work with Stadium Repos allows for upgrading them in a controlled manner. 

How to use and update application repos is described here: [Working with Stadium Repos](https://github.com/stadium-software/samples-upgrading)