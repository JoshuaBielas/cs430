# Names: Josh Bielas and Josh Garbi
# Lab: lab6 (NLP)
# Date: 3/4/2026

1. Looking at the attention matrix for layer 1, head 1, which token receives the most attention from the word "it"? Does this match your linguistic intuition about what "it" should refer to in the sentence? Why or why not?

    The word that receives the most attention from the word "it" is the word "is". This does not match our linguistic intuition because "it" should refer to a noun. Intuitive relationships don't always appear how they should in every layer of every head.


2. The [CLS] token often accumulates disproportionately high attention. What role does [CLS] play in BERT's architecture, and why might many tokens attend strongly to it even though it carries no dictionary meaning?

    The [CLS] token stores information from the whole sentence as sort of a summary. Many tokens attend strognly to it even though it carries no dictionary meaning because it has information about the whole input, so all tokens would attend to it. It ends up working as a key for the sentence because it has information about all of it. We did some research here: https://aditya007.medium.com/understanding-the-cls-token-in-bert-a-comprehensive-guide-a62b3b94a941

3. Attention is sometimes described as a "soft lookup" — rather than retrieving one fixed answer, the model blends information from many tokens weighted by relevance. How does this differ from how a traditional rule-based parser would resolve pronoun reference?

    It resolves pronoun references based on probability distributions instead of a guaranteed rule. This is better because in natural language certain procedures might be broken in other cases. It can be very hard to always know how two tokens will interact. It allows us to follow the correctness of a language that is hard to define by a set of rules.