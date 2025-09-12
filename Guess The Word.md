# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
This problem requires a strategy to find a secret word within a limited number of guesses. A simple approach of randomly guessing or linearly iterating through the word list is not guaranteed to work within the guess limit, especially if the number of words is large. The key is to make each guess as effective as possible by maximizing the information gained. 

The provided code implements a minimax-like strategy. The core idea is to choose a guess word that, in the worst case, eliminates the most potential candidates. The "worst case" for a guess is when it results in a match count that leaves the largest possible number of candidate words. By selecting a guess that minimizes this maximum possible size of the next candidate list, we make the most efficient progress toward finding the secret word. 

The intuition behind this is that if a guess partitions the remaining words into more evenly-sized groups based on the master.guess result, we are guaranteed to reduce the search space significantly, regardless of the actual secret word. A "bad" guess would be one that leaves a very large number of candidates for a particular match count, potentially slowing down the search process.

# Approach
<!-- Describe your approach to solving the problem. -->
The solution iteratively refines the list of possible words by making strategic guesses.
1. **Helper Function match(w1, w2):**
This function calculates the number of matching characters at the same position between two words, w1 and w2. This is a crucial component for filtering the word list after each guess.
1. **Main Loop:**
The algorithm runs in a while loop that continues as long as there are words left in the wordList.
- Selection of the Best Guess Word:
In each iteration, the code calculates a "score" for every word currently in wordList.
- The score of a word is the sum of match counts with all other words in the current wordList. This might seem counterintuitive at first glance. However, a word that has a high sum of matches with other words is less effective because it is more similar to many other potential candidates. A word with a low total number of matches with other words is more "unique" and therefore a better candidate for partitioning the word list effectively. The provided code actually finds the max score, which seems like the opposite of the minimax principle. A more robust implementation would follow the minimax strategy more closely by identifying a word that minimizes the maximum number of candidates remaining after any possible guess result.
- A more accurate and effective minimax strategy would be: for each potential guess word in wordList, calculate how many candidates would remain for each possible match count (0 to 6). Then, find the maximum of these counts for that word. The "best word" to guess is the one that minimizes this maximum count. This guarantees the best worst-case outcome.
3. **Guessing:**
The bestWord is passed to master.guess(), which returns the number of matches.
4. **Filtering:**
If matches == 6, the secret word has been found, and the function returns.
Otherwise, the wordList is filtered to create a new list candidates. Only words from the old wordList that have the same number of matches with bestWord as the matches count returned by master.guess() are kept. This is the core of the elimination process.
5. **Update:**
wordList is updated with the new candidates list, and the loop continues.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**O(N^2 * L),** where N is the number of words and M is the word length. Each iteration through the list checks matches.
- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**\(O(N\cdot L)\),** This is because the algorithm stores the wordList and the scoremap.

# Code
```python3 []
# """
# This is Master's API interface.
# You should not implement it, or speculate about its implementation
# """
# class Master:
#     def guess(self, word: str) -> int:

class Solution:
    def findSecretWord(self, words: List[str], master: 'Master') -> None:
        def match(w1, w2):
            count = 0
            for c1, c2 in zip(w1, w2):
                if c1 == c2:
                    count += 1
            return count

        wordList = words[:]
        while wordList:
            scoremap = {}
            for word in wordList:
                score = 0
                for otherWords in wordList:
                    if word != otherWords:
                        score += match(word, otherWords)
                scoremap[word] = score
            bestWord = max(wordList, key= lambda w: scoremap[w])
            matches = master.guess(bestWord)

            if matches == 6:
                return

            candidates = []
            for word in wordList:
                if matches == match(word, bestWord):
                    candidates.append(word)
                
            wordList = candidates
```
