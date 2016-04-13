# Mixin for adding Logical Delete to any Rails model

After writing this code across many many models in multiple Rails projects I figured it'd be good to generalize it as a Concern. This uses the Ruby Module's `included` hook to add a deleted_at field, a before_destroy hook that sets it, and changes the default_scope to only include models that have a nil deleted_at field.

```ruby
module LogicallyDeletable extend ActiveSupport::Concern

  included do
    field :deleted_at, type: DateTime
    before_destroy :logically_delete
    default_scope -> { where(deleted_at: nil) }
  end

  def logically_delete
    update_attribute(:deleted_at, DateTime.now.utc)

    return false
  end

  def deleted?
    !self.deleted_at.nil?
  end
end
```
