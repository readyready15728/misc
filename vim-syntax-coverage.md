# Vim Syntax Coverage
## Because I was curious

I want to start using Ruby instead of sed or other tools like it pretty much
exclusively for doing sophisticated command line fu. This was the first step
in that direction:

```ruby
pushd /usr/local/share/vim/vim82/syntax
ruby -ne 'puts $1 if /Language:\s+(.+)$/' *.vim | sort
```

Prints out every language Vim has syntax highlighting for. Quite a variety!
