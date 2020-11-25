# Memoized Factorial in Ruby
## I had a dream about this and had to write it down for some reason

```
class Integer
  @@memo = {0 => 1}

  def factorial
    return @@memo[self] if @@memo.include? self

    value = self * (self - 1).factorial
    @@memo[self] = value
    value
  end
end
```
