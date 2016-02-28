# Today I Learned!
Inspired by similar projects by other devs, I'm going to write down a thing that I've learned every day.

## February 2016

### 17th
Today I learned about member routes in Rails. It's an easy way to add routes to resources that might not be your basic RESTful routes. For example:

```ruby
  resources :submissions, only: [:show] do
    member do
      get :publish
      put :accepted
      put :rejected
      put :submitted_for_publishing
    end
  end
```

Will produce:

```bash
  publish_submission GET /submissions/:id/publish submissions#publishing
  ....
```

It's much less wordy than writing out things like:

```ruby
  get '/submissions/:id/publish' to: 'submissions#publish', as: submission_publish
```

### 24th
Today I learned that you can delete a remote git branch like so:

```bash
  git checkout old_branch
  git branch -m old_branch new_branch

  git push origin :old_branch

  git push origin new_branch
```
The `:` in front of the old branch name deletes the remote branch

### 29th (Leap day!)

Today I learned that, contrary to what Jon told me once, Rails' `render: 'partial_name'` and `render partial: 'partial_name'` are NOT the same.

When sending along local variables, it's probably a better idea to use `render partial: 'partial_name'`

Here's why:

  If you are using the term partial: in your render, for example like so:

  ```ruby
    = render partial: 'partial_name', locals: {foo: 'x', bar: 'y'}
  ```

  Then your locals will be available simply as foo and bar, directly:

  ```ruby
    = foo
    = bar
  ```

  The other syntax doesn't quite work like that! You need to access your variables in a different (uglier) way

  ```ruby
    render 'partial_name', locals: {foo: 'x', bar: 'y'}
  ```

  ```ruby
    = locals[:foo]
    = locals[:bar]
  ```