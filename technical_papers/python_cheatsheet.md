# Python Cheat Sheet (Strings, Lists, and Dictionary Methods)

## String Methods

- `lower()` —> Converts all characters to lowercase.
- `upper()` —> Converts all characters to uppercase.
- `strip()` —> Removes whitespace from both ends.
- `replace(old, new)` —> Replaces occurrences of one substring with another.
- `split(separator)` —> Splits a string into a list.
- `join(iterable)` —> Joins iterable elements into a single string.
- `find(value)` —> Returns the index of the first occurrence or `-1` if not found.
- `index(value)` —> Returns the index of the first occurrence and raises an error if not found.
- `startswith(prefix)` —> Checks whether the string starts with a given prefix.
- `isdigit()` —> Returns `True` if all characters are digits.

---

## List Methods

- `append(item)` —> Adds one item to the end of the list.
- `extend(iterable)` —> Adds all items from an iterable to the list at back of list.
- `insert(index, item)` —> Inserts an item at a specified index.
- `remove(item)` —> Removes the first occurrence of a specified item.
- `pop()` —> Removes and returns the last item by default.
- `pop(index)` —> Removes and returns the item at the specified index.
- `clear()` —> Removes all items from the list.
- `index(item)` —> Returns the index of the first occurrence of an item.
- `count(item)` —> Returns the number of occurrences of an item.
- `sort()` —> Sorts the list in ascending order by default, doesn't return new list.
- `reverse()` —> Reverses the order of items in the list.
- `copy()` —> Returns a shallow copy of the list.

---

## Dictionary Methods

- `get(key)` —> Returns the value of a key without raising an error if the key is missing.
- `get(key, default)` —> Returns a default value if the specified key does not exist.
- `keys()` —> Returns a view containing all dictionary keys.
- `values()` —> Returns a view containing all dictionary values.
- `items()` —> Returns a view containing all key-value pairs.
- `update(other)` —> Adds or updates key-value pairs from another dictionary or iterable.
- `pop(key)` —> Removes a key and returns its associated value.
- `popitem()` —> Removes and returns the last inserted key-value pair.
- `clear()` —> Removes all key-value pairs from the dictionary.
- `copy()` —> Returns a shallow copy of the dictionary.

---
- `sorted(iterable,key,reverse`) -> sorts and returns new list, doesn't modify </br> original object.Works with all iterable.
