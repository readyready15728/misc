# sort-puzzle-books.py
## Something I use for a "stash" of mine

```python
import os

with open('puzzle-books') as f:
    puzzle_books = [line.rstrip() for line in f.readlines()]

    for book in reversed(sorted(puzzle_books, key=lambda book: os.path.getmtime(book))):
        print(book)
```
