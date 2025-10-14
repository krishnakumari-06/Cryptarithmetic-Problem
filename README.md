<h1>ExpNo 8 : Solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python</h1> 
<h3>Name:    KRISHNA KUMARI E           </h3>
<h3>Register Number/Staff Id:   212224060127</h3>
<H3>Aim:</H3>
<p>
    To solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python
</p>
<h3>Procedure:</h3>
Input and Output
<br>Input:
This algorithm will take three words.
<br> B A S E<br>
    B A L L<br>
           ----------<br>
           G A M E S<br>

Output:
It will show which letter holds which number from 0 – 9.
For this case it is like this.

              B A S E                         2 4 6 1
              B A L L                         2 4 5 5
             ---------                       ---------
            G A M E S                       0 4 9 1 6
Algorithm
For this problem, we will define a node, which contains a letter and its corresponding values.<br>

isValid(nodeList, count, word1, word2, word3)<br>

Input − A list of nodes, the number of elements in the node list and three words.<br>

Output − True if the sum of the value for word1 and word2 is same as word3 value.<br>

Begin<br>
   m := 1<br>
   for each letter i from right to left of word1, do<br>
      ch := word1[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>
      val1 := val1 + (m * nodeList[j].value)<br>
      m := m * 10<br>
   done<br>

   m := 1<br>
   for each letter i from right to left of word2, do<br>
      ch := word2[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>

      val2 := val2 + (m * nodeList[j].value)
      m := m * 10
   done<br>

   m := 1<br>
   for each letter i from right to left of word3, do<br>
      ch := word3[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>

      val3 := val3 + (m * nodeList[j].value)
      m := m * 10
   done<br>

   if val3 = (val1 + val2), then<br>
      return true<br>
   return false<br>
End<br>
<hr>


# program
from itertools import permutations

def is_valid(mapping, word1, word2, word3):
    # Convert a word into a number based on the mapping of letters to digits
    def word_to_num(word):
        num = 0
        for ch in word:
            num = num * 10 + mapping[ch]
        return num
    
    val1 = word_to_num(word1)
    val2 = word_to_num(word2)
    val3 = word_to_num(word3)
    
    return val1 + val2 == val3

def solve_cryptarithmetic(word1, word2, word3):
    # Extract unique letters
    unique_letters = set(word1 + word2 + word3)
    
    if len(unique_letters) > 10:
        print("Too many unique letters, no solution possible with digits 0-9")
        return
    
    letters = list(unique_letters)
    
    # Leading letters cannot be zero
    leading_letters = set([word1[0], word2[0], word3[0]])
    
    digits = range(10)
    
    for perm in permutations(digits, len(letters)):
        mapping = dict(zip(letters, perm))
        
        # Check if any leading letter is assigned zero - invalid
        if any(mapping[lead] == 0 for lead in leading_letters):
            continue
        
        if is_valid(mapping, word1, word2, word3):
            print("Solution Found:")
            for letter in sorted(mapping.keys()):
                print(f"{letter} = {mapping[letter]}")
            
            # Display the sum
            val1 = int(''.join(str(mapping[ch]) for ch in word1))
            val2 = int(''.join(str(mapping[ch]) for ch in word2))
            val3 = int(''.join(str(mapping[ch]) for ch in word3))
            print(f"\n{word1} = {val1}")
            print(f"{word2} = {val2}")
            print(f"{word3} = {val3}")
            print(f"Verification: {val1} + {val2} = {val3}")
            return mapping
    
    print("No solution found.")

# output
<img width="353" height="378" alt="image" src="https://github.com/user-attachments/assets/aefbc8a5-f0e3-461a-9b28-c2916b465ba7" />

# Given problem: BASE + BALL = GAMES
solve_cryptarithmetic("BASE", "BALL", "GAMES")

<h2>Sample Input and Output:</h2>
SEND = 9567<br>
MORE = 1085<br>
<hr>
MONEY = 10652<br>
<hr>
<h2>Result:</h2>
<p> Thus a Cryptarithmetic Problem was solved using Python successfully</p>
