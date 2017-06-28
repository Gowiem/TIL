# Resolve/Reject a Promise without creating a new Promise

The RSVP lib provides standalone `resolve` and `reject` methods which come in handy when you're already dealing with promises. With these we don't need to wrap something that returns a promise to have our own resolve/reject behavior. See below:

```javascript
import Ember from 'ember';

const { RSVP } = Ember;
export default Ember.Component.extend({
  actions: {
    onValidate(model) {
      return model.validate({ on: ['form', 'patientId'] }).then(({ validations }) => {
        if (validations.get('isValid')) {
          return RSVP.resolve();
        } else {
          return RSVP.reject();
        }
      }, RSVP.reject);
    }
  }
});
```
