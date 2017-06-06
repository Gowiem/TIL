# 'Remember Me' Functionality with Ember Simple Auth

Storing user data in LocalStorage or Cookies is very simple with Ember Simple Auth, and that makes storing the user's 'remember me' preference along with their email super straight forward. Here is the code to do so:

```javascript
import Ember from 'ember';;
const { inject: { service }, on, isEmpty } = Ember;

export default Ember.Component.extend({
  session: service('session'),

  setup: on('init', function() {
    let loginData = this.get('session.data.login');
    if (!isEmpty(loginData)) {
      this.setProperties(loginData);
    }
  }),

  saveRememberMeState() {
    const { email, rememberMe } = this.getProperties('email', 'rememberMe');
    if (rememberMe) {
      this.set('session.data.login', { rememberMe: true, email: email });
    } else {
      this.set('session.data.login', { rememberMe: false, email: null });
    }
  },

  actions: {
    submit: function() {
      this.saveRememberMeState();
      // ...
  }
});
```
