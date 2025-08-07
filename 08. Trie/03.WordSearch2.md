Word Search II
Solved 
Given a 2-D grid of characters board and a list of strings words, return all words that are present in the grid.

For a word to be present it must be possible to form the word with a path in the board with horizontally or vertically neighboring cells. The same cell may not be used more than once in a word.

Example 1:
Input:
board = [
  ["a","b","c","d"],
  ["s","a","a","t"],
  ["a","c","k","e"],
  ["a","c","d","n"]
],
words = ["bat","cat","back","backend","stack"]

Output: ["cat","back","backend"]

Example 2:
Input:
board = [
  ["x","o"],
  ["x","o"]
],
words = ["xoxo"]

Output: []

Constraints:
1 <= board.length, board[i].length <= 12
board[i] consists only of lowercase English letter.
1 <= words.length <= 30,000
1 <= words[i].length <= 10
words[i] consists only of lowercase English letters.
All strings within words are distinct.


```java
// O(n^2)

class TrieNode {
    TrieNode[] children;
    boolean endOfWord;

    public TrieNode() {
        this.children = new TrieNode[26];
        this.endOfWord = false;
    }

    public void addWord(String word) {
        TrieNode curr = this;

        for (char ch : word.toCharArray()) {
            int i = ch - 'a';
            if (curr.children[i] == null) {
                curr.children[i] = new TrieNode();
            }
            curr = curr.children[i];
        }
        curr.endOfWord = true;
    }

    public void printTrie(TrieNode root, String prefix) {
        if (root.endOfWord) {
            System.out.println(prefix);
        }
        TrieNode curr = root;

        for (int i = 0;i < 26;i++) {
            if (curr.children[i] != null) {
                char ch = (char)('a' + i);
                printTrie(curr.children[i], prefix + ch);
            }
        }
    }
}

class Solution {
    private int ROWS, COLS;
    private int[][] directions = {{0, 1}, {0, -1},{1, 0}, {-1, 0}};
    private Set<String> result;
    private boolean[][] visit;

    public List<String> findWords(char[][] board, String[] words) {
        result = new HashSet<>();
        ROWS = board.length;
        COLS = board[0].length;
        visit = new boolean[ROWS][COLS];

        TrieNode root = new TrieNode();
        for (String word : words) {
            root.addWord(word);
        }
        root.printTrie(root, "");

        for (int r = 0;r < ROWS;r++) {
            for (int c = 0;c < COLS;c++) {
                dfs(board, root, r, c, "");
            }
        }        

        return new ArrayList<String>(result);
    }

    private void dfs(char[][] board, TrieNode node, int r, int c, String word) {
        if (r < 0 || c < 0 || r >= ROWS || c >= COLS || visit[r][c] || 
            node.children[board[r][c] - 'a'] == null) {
            return;
        }

        visit[r][c] = true;
        node = node.children[board[r][c] - 'a'];
        word += board[r][c];
        if (node.endOfWord) {
            result.add(word);
        }

        for (int[] dir : directions) {
            dfs(board, node, r + dir[0], c + dir[1], word);
        }

        visit[r][c] = false;
        
    }
    
}



```
