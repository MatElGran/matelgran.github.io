# Ruby blocks and anonymous positional arguments

From https://noelrappin.com/blog/2024/01/better-know-positional-arguments/

```ruby
def outer_method_with_params(*)
  %w[one two three].map { |*| puts * }
end
```

> This method behaves differently in Ruby 3.2 and Ruby 3.3.
> In Ruby 3.2, it is syntactically allowed, but the `*` in `puts *` is the argument to the outer method, not the argument to the block – the argument to the block is ignored.
> In Ruby 3.3 you get a syntax error, which is preferable, but it’s probably more preferable to have the block allow a passthrough. Maybe in Ruby 3.4.
