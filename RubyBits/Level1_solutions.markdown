# RUBY BITS PART 1:  CHALLENGES AND SOLUTIONS
---

## 1. UNLESS

### CHALLENGE
> We're putting together a system to manage our vast video game collection that we just can't seem to part with. Using if with negative conditions can be tough to read. Refactor the code below to use unless rather than if.

```ruby
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
if !games.empty?
  puts "Games in your vast collection: #{games.count}"
end
```

### SOLUTION

> Unless is more intuitive.

```ruby
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
unless games.empty?
  puts "Games in your vast collection: #{games.count}"
end
```
---

## 2. INLINE STATEMENTS

### CHALLENGE
> Doing a full unless statement is sometimes too much. Refactor the method below to use a single-line unless statement.


```ruby
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
unless games.empty?
  puts "Games in your vast collection: #{games.count}"
end
```


### SOLUTION

```ruby
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
puts "Games in your vast collection: #{games.count}" unless games.empty?
```
---

## 3. IMPLIED NIL
> Let's implement a simple search feature - for our naive implementation, we search for a game by its exact title, and if it's found, we show it. Comparing something with nil in an if statement isn't needed in Ruby. Refactor the code below to run without the nil comparison.

### CHALLENGE

```ruby
search = "Contra"
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
search_index = games.find_index(search)
if search_index != nil
  puts "Game #{search} Found: #{games[search_index]} at index #{search_index}."
else
  puts "Game #{search} not found."
end
```

### SOLUTION

```ruby
search = "Contra"
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
search_index = games.find_index(search)
if search_index
  puts "Game #{search} Found: #{games[search_index]} at index #{search_index}."
else
  puts "Game #{search} not found."
end
```
---

## 4. SHORT-CIRCUIT AND
> Let's clean up our code to make it search within each game title and show all the results. If it's an exact match, we'll show something special. Clean up the code below to short circuit the if statement.

### CHALLENGE

```ruby
search = "Super Mario Bros."
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
matched_games = games.grep(Regexp.new(search))

# Found an exact match
if matched_games.length > 0
  if matched_games.include?(search)
    puts "Game #{search} found."
  end
end
```

### SOLUTION


```ruby
search = "Super Mario Bros."
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
matched_games = games.grep(Regexp.new(search))

# Found an exact match
if matched_games.length > 0 && matched_games.include?(search)
  puts "Game #{search} found."
end
```
---

## 5. CONDITIONAL ASSIGNMENT

### CHALLENGE
> If no search is entered, we'll display all games. Notice the first line below where we're setting search to an empty string? Change this to use conditional assignment.

```ruby
search = "" unless search
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
matched_games = games.grep(Regexp.new(search))
puts "Found the following games..."
matched_games.each do |game|
  puts "- #{game}"
end
```

### SOLUTION

```ruby
search ||= ""
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
matched_games = games.grep(Regexp.new(search))
puts "Found the following games..."
matched_games.each do |game|
  puts "- #{game}"
end
```
---

## 6. CONDITIONAL RETURN I

### CHALLENGE
> Clean up the code below to only set search_result once by using a conditional return on the if statement.

```ruby
search = "Contra"
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
search_index = games.find_index(search)
if search_index
  search_result = "Game #{search} found: #{games[search_index]} at index #{search_index}."
else
  search_result = "Game #{search} not found."
end
puts search_result
```

### SOLUTION

```ruby
search = "Contra"
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
search_index = games.find_index(search)
search_result = if search_index
  "Game #{search} found: #{games[search_index]} at index #{search_index}."
else
  "Game #{search} not found."
end
puts search_result
```
---

## 7. CONDITIONAL RETURN II


### CHALLENGE
> One of the most common places to use conditional returns is within methods. Refactor the code below, removing the search_result variable all together.

```ruby
def search(games, search_term)
  search_index = games.find_index(search_term)
  search_result = if search_index
    "Game #{search_term} found: #{games[search_index]} at index #{search_index}."
  else
    "Game #{search_term} not found."
  end
  return search_result
end

games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
puts search(games, "Contra")
```

### SOLUTION

```ruby
def search(games, search_term)
  search_index = games.find_index(search_term)
  if search_index
    "Game #{search_term} found: #{games[search_index]} at index #{search_index}."
  else
    "Game #{search_term} not found."
  end
end

games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
puts search(games, "Contra")
```
---

## 8. SHORT-CIRCUIT EVALUATION

### CHALLENGE
> Using Short-Circuit Evaluation can clean up your code a great deal. Update the following method to use short circuit evaluation. While you're at it, why not try reducing the entire method to one line?

```ruby
def search_index(games, search_term)
  search_index = games.find_index(search_term)

  if search_index
    search_index
  else
    "Not Found"
  end
end
```

### SOLUTION

```ruby
def search_index(games, search_term)
  games.find_index(search_term) || "Not Found"
end
```
---
