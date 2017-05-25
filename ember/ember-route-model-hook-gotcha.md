# Ember Router model hook not being called gotcha

I've run into this a few times and I always forget because it is not exactly intuitive and browsing the guides isn't that helpful (you need to know what you're looking for). The basic issue is that providing the full model to the `link-to` helper causes the route that is being linked to not run it's `model` hook. If important data is being fetched alongside the given model/model ID in the `model` hook (such as when loading multiple model via `RSVP.hash`) then this can be a problem. To get around this in an asynchronous way the simplest path forward is to use `link-to` and only provide the given model's id as the final dynamic segment. For example:

```javascript
// This will not fire the model hook. The submission will be the 'model' for the route
{{#link-to 'form.submissions.review' submission.form submission}}Review{{/link-to}}

// This will fire the model hook with the submission id in the params hash if specified by the router DSL.
{{#link-to 'form.submissions.review' submission.form submission.id}}Review{{/link-to}}
```
