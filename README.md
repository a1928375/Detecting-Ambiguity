# Detecting-Ambiguity

A grammar is ambiguous if there exists a string in the language of that grammar that has two (or more) parse trees. Equivalently, a grammar is ambiguous if there are two (or more) different sequences of rewrite rules that arrive at the same final string. Ambiguity is a critical concept in natural languages and in programming languages. If we are not careful, our formal grammars for languages like JavaScript will have ambiguity. In this problem you will write a procedure isambig(grammar,start,tokens) that takes as input a grammar with a finite number of possible derivations and a string and returns True (the value True, not the string "True") if those tokens demonstrate that the grammar is ambiguous starting from that start symbol (i.e., because two different sequences of rewrite rules can arrive at those tokens). For example: 

      grammar1 = [                  # Rule Number
                  ("S", [ "P", ] ),       # 0
                  ("S", [ "a", "Q", ]) ,  # 1
                  ("P", [ "a", "T"]),     # 2
                  ("P", [ "c" ]),         # 3
                  ("Q", [ "b" ]),         # 4
                  ("T", [ "b" ]),         # 5
                  ] 

In this grammar, the tokens ["a", "b"] do demonstrate that the grammar is ambiguous because there are two difference sequences of rewrite rules to obtain them:  

        S  --0->  P  --2->  a T  --5->  a b 

        S  --1->  a Q  --4->  a b 

The two sequences are [0,2,5] and [1,4]. However, the tokens ["c"] do _not_ demonstrate that the grammar is ambiguous, because there is only one derivation for it: 

        S  --0->  P  --3->  c

        So even though the grammar is ambiguous, the tokens ["c"] do not demonstrate that: there is only one sequence [0,3]. 

Important Assumption: In this problem the grammar given to you will always have a finite number of possible derivations. So only a
finite set of strings will be in the language of the grammar. (You could test this with something like cfginfinite, so we'll just assume it.) 

       Hint 1: Consider something like "expand" from the end of the Unit, but instead of just enumerating utterances, enumerate 
       (utterance,derivation) pairs. For a derivation, you might use a list of the rule indexes as we did in the example above. 

       Hint 2: Because the grammar has only a finite number of derivations, you can just keep enumerating new (utterance,derivation) 
       pairs until you cannot find any that are not already enumerated.
