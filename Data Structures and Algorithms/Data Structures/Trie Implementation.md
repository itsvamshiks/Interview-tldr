### Implement the Trie class:

 - Trie() Initializes the trie object.
 - void insert(String word) Inserts the string word into the trie.
 - boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
 - boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.

```
class TrieNode {
    
    private TrieNode[] links;
    private final int R = 26;
    
    private boolean isEnd;
    
    public TrieNode(){
        links = new TrieNode[R];
    }
    
    public boolean containsKey(char ch){
        return this.links[ch - 'a'] != null;
    }
    
    public TrieNode get(char ch){
        return this.links[ch-'a'];
    }
    
    public void put(char ch,TrieNode node){
        this.links[ch - 'a'] = node;
    }
    
    public boolean isEnd(){
        return this.isEnd;
    }
    
    public void setEnd(){
        this.isEnd = true;
    }
    
}

class Trie {
    
    private TrieNode root;

    public Trie() {
        
        this.root = new TrieNode();
        
    }
    
    public void insert(String word) {
        
        TrieNode curr = this.root;
        
        for(int i = 0;i < word.length();i++){
            char currentChar = word.charAt(i);
            if(!curr.containsKey(currentChar))
                curr.put(currentChar,new TrieNode());
            
            curr = curr.get(currentChar);
        }
        
        curr.setEnd();
        
    }
    
    public TrieNode searchPrefix(String word){
        TrieNode curr = this.root;
        
        for(int i = 0;i < word.length();i++){
            char currentChar = word.charAt(i);
            if(curr.containsKey(currentChar))
                curr = curr.get(currentChar);
            else
                return null;
        }
        
        return curr;
        
    }
    
    
    
    public boolean search(String word) {
        TrieNode node = searchPrefix(word);
        return node!=null && node.isEnd();
        
        
    }
    
    public boolean startsWith(String prefix) {
        
        TrieNode node = searchPrefix(prefix);
        return node!=null;
        
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
