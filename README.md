Basic setup:
===
- Include validator.js just before the closing </body> tag;
- Add native validation markup in forms - that means to add some of the following properties from the HTML 5 spec:
  - **required** - the field cannot be empty
  - **min-length** - minimum length of value
  - **max-length** - maximum length of value
  - **min** - minimum value
  - **max** - maximum value
  - **type** - the type of the input (checks if the value is valid for this input type)
  - **pattern** - the regEx pattern used to validate the value of the input. When setting pattern, the input must have **title** attribute explaining the required format for that particular field.

Additionally you can use the **data-match** attribute to check if the value of the input is the same as the value of another input. 

Keep in mind that all inputs are required to have unique id attribute, or the validator will return unexpected results.


Use cases:
===

Basic validation of all forms:
---
`
var validator = new Validator(); // Initialize Validator
`
`
validator.validate(); // start validation of all forms
`
This will validate all forms on the page on submit and in real time.

Validation of single form:
---
`validator.validateForm(form); // where form is the form element to be validated
`

Validating single element:
---
`validator.validateElement(element); // where element is the input to be validated
`

Checking if element's value is valid:
---
`
validator.isValid(element);// returns true or false if the value of element is valid.
`

Validating multi-step form:
---
Every step from the form should be **<fieldset>**  element. 
You can check if every single fieldset is valid by using the method provided for validating single form. So it would look like this:
`
var step1 = document.getElementById('step1');
var step2 = document.getElementById('step2');
var step3 = document.getElementById('step3');
if(validator.validateForm('step1')) { showStep2(); }
if(validator.validateForm('step1') && validator.validateForm('step2')) {
    showStep3();
}
`

Validation using reCaptcha:
---
First you must load the recaptcha API (https://www.google.com/recaptcha/api.js?onload=onloadCallback&render=explicit)

Load validator, and initialize it (var validator = new Validator();)

you must create function called **onloadCallback** and inside chain the validator methods like this:
`validator.recaptcha('recaptcha-key').validate();`
where recaptcha-key is your api key.



Sample use:
===
`
<form action="submit.php">
    <input required type="email" id="email">
    <input required type="password" id="password" min-length="6" max-length="100">
    <input required type="password" id="passwordConfirm" data-match="password">
    <button type="submit">Submit</button>
</form>
`

</> with <3 @ [Code Nest](https://code-nest.com)
