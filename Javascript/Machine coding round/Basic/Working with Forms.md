Contact form with action and method defined

Action is where the form data is submitted while the method determines the http used to submit the form data.
Question:
Building forms is a common task in Front End. In this exercise, we will build a basic "Contact Us" form, commonly seen on marketing websites for visitors to ask questions or provide feedback.

## Requirements

- The form should contain the following elements:
    - Name field.
    - Email field.
    - Message field. Since the message can be long, a `<textarea>` will be more suitable.
    - Submit button
        - Contains the text "Send".
        - Clicking on the submit button submits the form.
    - Drop down as well
- The form and submission should be implemented entirely in HTML. Do not use any JavaScript or framework-specific features for this question.
- There is no need to do any client-side validation on the fields. Validation will be done on the server side.

## Submission API

Upon submission, `POST` the form data to `https://www.greatfrontend.com/api/questions/contact-form` with the following fields in the **request body**: `name`, `email`, `message`, options.

If all the form fields are correctly filled up, you will see an alert containing a success message. Congratulations!

## Notes

You do not need JavaScript for this question, the focus is on HTML form validation and submission.

```js
import submitForm from './submitForm';

  

export default function App() {

  return (

    <form
  onSubmit={submitForm}
  method="post"
  action="https://www.greatfrontend.com/api/questions/contact-form"
>
  <div>
    <label htmlFor="name">Enter your Name: </label>
    <input type="text" name="name" id="name" />
  </div>

  <div>
    <label htmlFor="email">Enter your Email: </label>
    <input type="email" name="email" id="email" />
  </div>

  <div>
    <label htmlFor="message">Message: </label>
    <textarea name="message" id="message" rows="4" cols="40"></textarea>
  </div>

  <div>
    <label htmlFor="options">Select an Option: </label>
    <select name="option" id="options">
      <option value="">-- Choose --</option>
      <option value="feedback">Feedback</option>
      <option value="support">Support</option>
      <option value="inquiry">Inquiry</option>
    </select>
  </div>

  <button type="submit">Send</button>
</form>


  );

}
```


![[Pasted image 20250502121357.png]]


```js
const SUBMIT_URL =

  'https://www.greatfrontend.com/api/questions/contact-form';

  

export default async function submitForm(event) {

  event.preventDefault();

  const form = event.target;

  

  try {

    if (form.action !== SUBMIT_URL) {

      alert('Incorrect form action value');

      return;

    }

  

    if (form.method.toLowerCase() !== 'post') {

      alert('Incorrect form method value');

      return;

    }

  

    const formData = new FormData(form);

    const response = await fetch(SUBMIT_URL, {

      method: 'POST',

      headers: {

        'Content-Type': 'application/json',

      },

      body: JSON.stringify({
  name: formData.get('name'),
  email: formData.get('email'),
  message: formData.get('message'),
  option: formData.get('option'),         // for single select
  options: formData.getAll('options'),    // for multi-select
}),

    });

  

    const text = await response.text();

    alert(text);

  } catch (_) {

    alert('Error submitting form!');

  }

}
```