## Accessibility Considerations of Form and Validation 
* Focus must be set to the error related field when error occur.
* Error message must be programmatically determined with the associated field to describe user in text.
* Form must have programmatically determiable label.
* Label should be always visible.
* Labels should be close proximity to their associated fields.
* Label should be meaningful. 
  
### Terminology
* aria-describedby="id" Programmatically determined error message with associated field
* ref="id" Define the target of sending focus
* v-model: Two ways binding of forms and data
* role="alert": Make announcement for screen reader of success message.
* `<label for="label-id">Label: <label>` `id="label-id"`: Provide explicit label
* `aria-invalid`: Intimate screen reader about form validity.
* `aria-required`: Intimate screen reader form field is required but no validation.
* `@input="validateField('name')"`: `@input` sets up an event listner for the `input` event `validateField('name')` is the method being called. When the input event is triggered, this method will be executed with 'name' as the argument.

