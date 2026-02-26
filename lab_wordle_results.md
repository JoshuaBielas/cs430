# Names: Josh Bielas and Josh Garbi
# Lab:  (lab Wordle)
# Date: 2/19/2026


1. In the constraint propagation example, explain the relationship between the pattern encoding and the reduction in state space. How does each piece of information (gray, yellow, green) contribute differently to narrowing possibilities?

    The pattern encoding gives possible groups of states to eliminate that don't match the encoded pattern. All states that don't match the pattern are eliminated. A gray eliminates all states that use that letter. A yellow eliminates all states that use that letter in the location it is yellow. A green eliminates all states that don't have that letter in that location.

2. The feedback mechanism is deterministic—the same guess against the same answer always produces the same pattern. How does this property affect the agent strategies we'll explore? Would probabilistic feedback change the problem fundamentally?

    If it were to be probabilistic, then if we guessed a word with the same letters in the same spot it wouldn't necessarily be eliminated. With it being deterministic, All states with the same pattern that doesn't match would be eliminated. If it were probabilistic, way less states would be removed for each guess. 

3. The frequency agent uses a "greedy" approach—it always picks what seems best locally without considering future moves. Describe a scenario where this could lead to suboptimal performance compared to an agent that thinks ahead.

    If it is choosing the best choice locally based on letter frequencies. There could be suboptimal performance in cases where the target word uses many letters that have low frequencies. Thinking ahead would be better in this case. 

4. Notice how the unique letter bonus affects word selection. Why might choosing words with five distinct letters be advantageous in early guesses but potentially wasteful in later guesses?

    In early guesses it can be beneficial to learn as much information about new letters as possible, so you can narrow down what letters are in the word and what letters aren't. In later guesses, it is important to start placing letters in their correct locations, so it isn't beneficial to guess all new letters. 

5. This agent recalculates frequencies based on the remaining word list after each guess. How does this adaptive behavior differ from using fixed, pre-computed frequencies? What are the computational trade-offs?

    The adaptive behavior eliminates from the state space at a higher rate than non adaptive. If we find out where a letter is in the word, we can narrow down to words with the best frequencies with that letter in that location. The trade-offs are that you have to calculate the frequencies for each guess. The benefit is you will likely have less guesses.

6. Entropy measures how evenly a guess partitions the remaining possibilities. Explain why a guess that splits possibilities into equally-sized groups has higher entropy than one that creates very uneven partitions. Use a concrete example from the output.

    A guess that splits possibilities into equally-sized groups causes us to have more uncertainty because there are many word possibilities within each of these groups. We don't have any groups that have less uncertainty than the others. For the first word when we guess DITER, it is split it into relatively equal groups. This has a high entropy. When we guess CIDER where we are just trying to figure out one more letter and splitting into uneven partitions the entropy is relatively low.

7. The entropy agent might choose a word that cannot possibly be the answer if it maximizes information gain. Is this rational? Discuss the trade-off between "playing to win immediately" versus "playing to gather information."

    Yes, this is rational. It can guess a word that has more unknowns in it, so that it gains more information to be more certain of the word on a future guess. If it doesn't split groups evenly, and it is in a group that the solution isn't it is wrong. Playing to win immediately may help you to get the word faster in some cases, but you may have to get lucky. When you play to gather information, it may take longer to guess the word, but you are more likely to guess it because there is less uncertainty.

8. Compare the computational complexity of the frequency heuristic versus entropy calculation. As the word list grows larger, which approach scales better and why? What does this tell us about the trade-off between optimality and feasibility?

    The frequency heuristic approach would scale better to larger word lists because the letter frequencies are already established and won't change as words are added. With the entropy calculatiom, we have to iterate over all words in the word list which takes more computations and time. Frequency is more feasable and less optimal. Entropy is more optimal and less feasable. We have to trade frequency for optimality and optimality for frequency.

9. The minimax agent provides a guarantee: "No matter what the answer is, I'll have at most X words remaining after this guess." Why might this guarantee be valuable in competitive or time-limited scenarios even if average performance is worse?

    It is valuable because it doesn't rely on feedback to narrow down the remaining choices left. It doesn't care about what the word could be; it just wants to narrow down the maximum remaining words. Entropy and Frequency try to calculate what word to use next. Minimax is faster than Entropy is. It wants to narrow down the worst case which is important when it is important that you make sure you guess the word. If finishing quicker is better than an ideal solution it would outperform entropy. 

10. Observe cases where entropy and minimax choose different first words. Describe the philosophical difference in these strategies: one is optimistic (optimizing average case) and one is pessimistic (optimizing worst case). Which worldview seems more appropriate for Wordle, and why?

    Minimax optimizes worst case and entropy optimizes average case. Minimax would be better for Wordle because when optimizing its worst case it will perform better overall. In Wordle it is more important that you get the word in the certain number of guesses rather than how many guesses it takes you to get the word. Pessimistic would be better for wordle because there isn't an opponent. It is just probability. There could be scenarios where entropy chooses a word that seems less optimal at the time but reveals more information than minimax.

11. As the number of remaining possibilities decreases (e.g., down to 2-3 words), do you notice the strategies converging? Explain why different optimization criteria matter more when uncertainty is high versus low.

    Entropy and minimax often converge as the remaining possibilities decreases. When uncertainty is high, how you optimize will remove larger amounts of words. When you have lots of words remaining, you want a strategy that narrows them down the quickest. When you have less words remaining, it doesn't matter as much what strategy you use because you are more trying to guess the word at this point rather than narrow down the remaining options. 

12. The hybrid agent switches strategies mid-game. Describe what fundamentally changes about the problem when you have 10 remaining possibilities versus 2 remaining possibilities that justifies this strategy change.

    When you have more than 10 remaining possibilities, entropy is very high. When you have 2 possibilities, entropy is low. When you have fewer remaining possibilities, it is more efficient to pick the most likely one rather than eliminating what it isn't. 

13. The threshold parameter (when to switch strategies) is somewhat arbitrary. Propose a method for automatically determining the optimal threshold based on the statistical properties of the word list. What factors should influence this decision?

    Entropy could attempt to break up the remaining possibilities again, but if it isn't able to eliminate enough it might switch. Entropy could pass over to minimax when the entropy value reaches a specific level rather than when the words remaining reaches a specific level.

14. Could we extend this hybrid approach to three or more strategies? Sketch out a meta-strategy that might incorporate frequency heuristics, entropy, and minimax at different stages. What would be the benefits and costs?

    We could expand this hybrid approach to three or more strategies. A new idea might be to use frequency for the first guess to get a good first guess. Then we could use entropy for a period of time. Then we can end with minimax as we get closer to the final guess. This would use each of the strategies for their best case uses. 

15. Examine the average versus worst-case performance across strategies. Does the "best on average" strategy also have the "best worst case"? Discuss why optimization criteria matter when choosing between algorithms.

    Yes, it does have the best worst case. We had entropy and hybrid be 4.00 in the average case and both were 4 in the max case. Which was the best. Choosing lower optimization criteria will increase the success rate over time. 

16. The benchmark uses a random sample of words. How might results differ if we tested on: (a) only common words, (b) words with unusual letter patterns, or (c) the full 12,000+ word dictionary? What does this reveal about the generalizability of our findings?

    If we tested on common words, frequency would probably do better. If we tested on words with unusual letter patterns, entropy and minimax would do better than frequency. Entropy may outperform minimax because it won't perform worse while the other agents might. For the full 12000+ word dictionary, the agents will encounter some common words and some more complex words. They will perform similarly to how they would on a random sample of words. Hybrid will probably perform the best in all cases. If we know the structure of our input, we can choose a model accordingly. In general we will be working with words from the full 12,000+ word dictionary which means we will have some common and some more complex words. 

17. Notice the computational time differences between strategies. In a real-time game where players have limited thinking time, how should we balance solution quality against computation speed? Propose a practical decision rule.

    The current implementation of a hybrid agent wouldn't work because it takes a long time. Entropy performed just as well as it and was a lot faster, so we might be better off to use entropy. A good approach would probably be to start with frequency for a guess or two and then switch to entropy and then minimax. In the case where a longer running model would perform better, we could choose a quick but less precise model in the beginning to get most of the way. Then we could finish the problem with a slower model with better performance.

18. Traditional RL requires millions of training episodes to learn Wordle strategy. Modern LLMs appear to play reasonably well without explicit training on Wordle. What does this suggest about how these models represent and transfer knowledge across different tasks?

    They appear to be pretty good at transferring knowledge from other tasks to wordle. A general algorithm for language can be applied to more specific problems such as wordle because wordle is about pattern similarities which is similar to structuring language sentences. LLMs are trained on lots of puzzles and strategic reasoning. They know how to use strategy in many ways to solve diverse problems.

19. Compare the transparency of the rule-based agents (entropy, minimax) versus the RL/LLM agent. Which approach makes it easier to understand why a particular guess was chosen? Discuss the trade-off between interpretability and performance.

    The RL/LLM agent is more complicated and has more of a black box approach. This means it is hard to determine how it arrives at its conclusions. With the rule-based agents we know what it is doing and can see it happening. Less interpretable agents often have better performance as seen by the RL/LLM approach.

20. The RL agent needs to balance exploration (trying suboptimal guesses to learn) versus exploitation (using its current best strategy). How do the deterministic agents we built earlier handle this trade-off implicitly through their optimization criteria?

    The deterministic agents use categorical guesses to narrow down the remaining guess list. These guesses may not be similar to the result, but they eliminate large groups of words that they also contain letters for. Their goal is to narrow down the number of possible guesses.

21. Words with repeated letters (like "ATONE" with two instances of a vowel) challenge our agents differently. Explain why repeated letters reduce the information gained per guess and how this affects entropy calculations.

    When the word has repeated letters and we guess one of the letters, we only gain information about one of that letter. We don't know whether there is more than one of that letter in the word still. If we make a guess that has two of the same letter in it, we gain less information because we only learn about 4 letters rather than 5 from the guess. This affects entropy calculations because a word with two instances of a vowel separates groups less evenly and gives higher entropy. 

22. When multiple words remain that differ by only one letter (like "STARE", "SCARE", "SPARE"), the game becomes partially luck-based. Discuss how each strategy (frequency, entropy, minimax) handles this degeneracy and whether any approach is fundamentally superior in these cases.

    Frequency will choose the letter that appears most frequently. Entropy will try to make a guess that helps it gain the most information, but in this case each guess would cause it to gain the same amount of information. It would just choose the word that comes first. Minimax wants to make a guess that will improve the worst case the most, but all words will return the same size partitions, so it will also just choose the word that comes first. Frequency would be superior in this case because it actually has information that it bases its choice off of rather than just choosing the first option.

23. Consider the broader implications: Wordle has a finite, known state space (12,000+ words). How would these strategies need to adapt for a game with an unknown or infinite state space (like Scrabble or real-world decision problems)? What assumptions would break down?

    If we have infinite state space, the agents that try to group, eliminate, or narrow down would fail because they wouldn't be able to narrow down an infinite amount of states. Frequency also wouldn't work because the frequency values would be meaningless with an infinite amount of states because they would all be out of infinity, so essentially 0. The assumptions that guesses would narrow down state space breaks down with an infinite state space.