# Level 01: EXPRESSIONS
---

## INTRO
Purpose of the course is to give feel for more advanced features in *RUBY*.

## UNLESS

```ruby
if ! tweets.empty?
  puts "Timeline:"
  puts tweets
end
```

Ruby has a more expressive way of doing this:

```ruby
unless tweets.empty?
  puts "Timeline:"
  puts tweets
end
```

If the example has an else statement, things get confusing.  Use *IF* with *ELSE*.

## NIL IS FALSE-Y

In Ruby, nil is treated as false.

```ruby
if attachment.file_path != nil
  attachment.post
end
```

```ruby
if attachment.file_path
  attachment.post
end
```

Be careful with conditional statements, not all things that you *THINK* are *false*, will be evaluated as *false*.

  "" treated as true
  0  treated as true
  [] treated as true

```ruby
unless name.length
  warn "User name required"
end
```

Even if *name.length* is == 0, the code will never be run because the conditional will evaluate to *true*.

## INLINE CONDITIONALS

This would work:

```ruby
if password.length < 8
  fail "Password too short"
end
unless username
  fail "No user name set"
end
```

But this would be a good time to use the *inline conditional*:

```ruby
fail "Password too short" if password.length < 8
fail "No user name set" unless username
```

## SHORT-CIRCUIT "AND"

```ruby
if user
  if user.signed_in?
    #...
  end
end
```

```ruby
if user && user.signed_in?
  #...
end
```

## SHORT-CIRCUIT ASSIGNMENT

```ruby
result = nil || 1 # -> 1
result = 1 || nil # -> 1
result = 1 || 2   # -> 1
```

If the first part evaluates to *true*, then the second part will never get evaluated.

## DEFAULT VALUES - "OR"

```ruby
tweets = timeline.tweets
tweets = [] unless tweets
```

A bettew way uses the short circuit:

```ruby
tweets = timeline.tweets || []
```

## SHORT-CIRCUIT EVALUATION

```ruby
def sign_in
  current_session || sign_user_in
end
```

This will check if there is a current_session and if not then it will require the user to sign in.

## CONDITIONAL ASSIGNMENT

Another way to use the OR symbols is with an equal sign to do conditional assignment:

```ruby
i_was_set = 1
i_was_set ||=2

puts i_was_set
```

Returns 1.  Assigns IF there's no existing value.

```ruby
i_was_not_set ||=2

puts i_was_not_set
```

Returns 2

```ruby
options[:country] = 'us' if options[:country].nil?
options[:privacy] = true if options[:privacy].nil?
options[:geotag] = true if options[:geotag].nil?
```

Use the conditional assignment operator to assign values to these variables if they are *nil*.

```ruby
options[:country] ||= "us"
options[:privacy] ||= true
options[:geotag] ||= true
```

## CONDITIONAL RETURN VALUES

```ruby
if list_name
  options[:path] = "/#{user_name}/#{list_name}"
else
  options[:path] = "/#{user_name}"
end
```

In Ruby conditionals always return a value.  The options path can be moved in front of the conditional, the vallues that get returned from the conditionals will be sent to it:

```ruby
options[:path] = if list_name
  "/#{user_name}/#{list_name}"
else
  "/#{user_name}"
end
```

```ruby
def list_url(user_name, list_name)
  if list_name
    "https://twitter.com/#{user_name}/#{list_name}"
  else
    "https://twitter.com/#{user_name}"
  end
end
```

## CASE STATEMENT VALUE

```ruby
client_url = case client_name
  when "web"
    "http://twitter.com"
  when "Facebook"
    "http://www.facebook.com/twitter"
  else
    nil
end
```

Even *case* returns a value.

*case* can be used with a *range*:

```ruby
popularity = case tweet.retweet_count
  when 0,,9
    nil
  when 10..99
    "trending"
  else
    "hot"
end
```

Or with *regular expressions*:

```ruby
tweet_type = case tweet.status
  when /\A@\w+/
    :mention
  when /\Ad\s+\w+/
    :direct_message
  else
    :public
end
```

One last way to write this statement:

```ruby
tweet_type = case tweet.status
  when /\A@\w+/       then :mention
  when /\Ad\s+\w+/    then :direct_message
    else                   :public
end
```
