# Flash Messages

This example Sinatra application that implements "flash" messages using [`Rack::Flash`](https://github.com/treeder/rack-flash).

A "flash" message is a temporary message that is passed from one request (A) to another (B), but disappears after the subsequent request (B) has been handled.

For example, if you have these routes:

```ruby
get '/' do
  flash[:my_message]
end

post '/message' do
  flash[:my_message] = 'Hello!'
  redirect '/'
end
```

You could send a `POST` request to `/message`, be redirected to `/`, and you receive a response with body `'Hello!'`. A subsequent `GET` request to `/` would _not_ have any values at `flash[:my_message]` though.

Flash messages are useful for addressing a variety of situations where you need a message passed between requests. For example:

- Notifying a user of errors when attempting to persist a resource
- Showing a welcome message after logging in
- Displaying a confirmation message when a user action is successful

## Running The Application

Make sure you're in the `public-file-upload` directory.  Once there, run the following two commands to configure your application correctly:

```text
$ bundle install --without production
$ rake setup:dotenv
```

### On Cloud9

If you're using [Cloud9](http://c9.io), run the application with

```
$ rerun bundle exec ruby app-flash-messages.rb -p $PORT -o $IP
```

### On Your Own Computer

If you're on your own computer, run the application with

```
$ rerun bundle exec rackup
```

If everything runs successfully, you should be able to visit <http://localhost:4567> and see the web application.
