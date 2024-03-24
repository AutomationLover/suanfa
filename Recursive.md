# name
递归

## when using


## template


## examples
```python

def isMatch(s, p):
    if not p:
        return not s
    if not s:
        if p[-1] == '*' and len(p) > 1:
            return isMatch(s, p[:-2])
        return False

    def last_letter_match(s_member, p_member):
        return s_member == p_member or p_member == '.'

    if p[-1] == '*' and len(p) > 1:
        return isMatch(s, p[:-2]) or \
               (last_letter_match(s[-1], p[-2]) and isMatch(s[:-1], p))
    elif last_letter_match(s[-1], p[-1]):
        return isMatch(s[:-1], p[:-1])
    else:
        return False


def test():
    # Test cases
    print(isMatch("aa", "a")) # Output: False
    print(isMatch("aa", "a*")) # Output: True
    print(isMatch("ab", ".*")) # Output: True


```

```python
# https://leetcode.cn/problems/concatenated-words/submissions/514458661/?company_slug=microsoft
472. 连接词 - 力扣（LeetCode）

from collections import defaultdict

def findAllConcatenatedWordsInADict(words):
    def is_concatenated(word, word_dict, memo):
        if word in memo:
            return memo[word]

        for i in range(1, len(word)):
            prefix = word[:i]
            suffix = word[i:]

            if prefix in word_dict and (suffix in word_dict or is_concatenated(suffix, word_dict, memo)):
                memo[word] = True
                return True

        memo[word] = False
        return False

    word_dict = set(words)
    memo = {}
    result = []

    for word in words:
        if is_concatenated(word, word_dict, memo):
            result.append(word)

    return result

# Example usage
words = ["cat", "cats", "catsdogcats", "dog", "dogcatsdog", "hippopotamuses", "rat", "ratcatdogcat"]
print(findAllConcatenatedWordsInADict(words))

```


```python
from collections import OrderedDict

def normalize_json(json_obj):
    def flatten(obj, parent_key='', sep='.'):
        items = []
        if isinstance(obj, dict):
            sorted_items = sorted(obj.items(), key=lambda x: x[0])
            for key, value in sorted_items:
                new_key = parent_key + sep + key if parent_key else key
                items.extend(flatten(value, new_key, sep).items())
        elif isinstance(obj, list):
            for idx, value in enumerate(obj):
                new_key = parent_key + sep + str(idx) if parent_key else str(idx)
                items.extend(flatten(value, new_key, sep).items())
        else:
            items.append((parent_key, obj))
        return OrderedDict(items)

    return flatten(json_obj)

json_obj = {
    "name": "John Doe",
    "age": 30,
    "address": {
        "street": "123 Main St",
        "city": "Anytown",
        "state": "CA"
    },
    "hobbies": ["reading", "hiking", {"sport": "tennis"}]
}

normalized_json = normalize_json(json_obj)
print(normalized_json)
OrderedDict([('age', 30), ('address.city', 'Anytown'),
             ('address.state', 'CA'), ('address.street', '123 Main St'),
             ('hobbies.0', 'reading'),
             ('hobbies.1', 'hiking'),
             ('hobbies.2.sport', 'tennis'),
             ('name', 'John Doe')])

```