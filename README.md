# recaptcha-tester

A simple page that generates ReCaptcha V2 challenges, to test your backend.

## How to use

- In your ReCaptcha's settings, add `humodz.github.io` to the allowed domain
- (Optional) if you want to generate lots of ReCaptcha challenges, reducing the ReCaptcha difficulty will make it faster.
- Go to [](https://humodz.github.io/recaptcha-tester/), fill the text box with your **Site Key** (**NOT** your secret key), and press **Create ReCaptcha*
- After you solve the ReCaptcha, the returned challenge string will appear in **Challenge result**
- To generate another one, click **Reset ReCaptcha**

## How do I validate a ReCaptcha challenge?

Sample Node.js code (uses the `recaptcha-verify` library):

```js
const Recaptcha = require('recaptcha-verify');

function validateRecaptcha(challengeResult) {
  const recaptcha = new Recaptcha({
    secret: 'the secret key from the ReCaptcha admin console',
    verbose: false,
  });

  return new Promise((resolve, reject) => {
    recaptcha.checkResponse(challenge, (error, response) => {
        // Couldn't verify (maybe a network error?)
        if (error) {
            return reject(error);
        }

        // Success is a boolean, true = valid challenge, false = invalid challenge
        return resolve(response.success);
    });
  });
}
```