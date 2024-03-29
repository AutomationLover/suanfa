# name


## when using


## template
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False
        self.word = None
        self.prefix_count = 0
    
    
class Trie:
    def __init__(self):
        self.root = TrieNode()
        
    def get_root(self):
        return self.root
    
    def insert(self, word):  # O(L)
        node = self.root
        for i in range(len(word)):
            if word[i] not in node.children:
                node.children[word[i]] = TrieNode()
            node = node.children[word[i]]
            node.prefix_cound += 1
        
        node.is_word = True
        node.word = word
        
        
class WordDictionary:
    def __init__(self):
        self.trie = TrieNode()
    
    def add_word(self, word):
        self.trie.insert(word)
        
    def search(self, word):
        return self.dfs(self.trie.get_root(), word, 0)
    
    def dfs(self, root, word, index):
        if index == len(word):
            return root.is_word
        letter = word[index]
        if letter == '.':
            for child in root.children:
                if self.dfs(root.children[child], word, index + 1):
                    return True
            return False
        
        if letter in root.children:
            return self.dfs(root.children[letter], word, index + 1)
        
        return False
```

```python

```

## examples
