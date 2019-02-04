## Pointer Networks

### Problem solved
Sequence-to-sequence where the output sequence is some sequence of
indices. Examples: sorting a sequence (not covered), convex hull, TSP,
Delaunay Triangulation


### What?
1. Sequence to sequence architecture
	1. Inputs: some sequence of tokens
	2. Outputs: some other sequence of tokens!
	3. Common examples: NMT,
	4. This is different from sentence classification (sentiment analysis, labelling, etc.) - fixed set of classes (here - we produce a sequence)
		Also, different from POS tagging, etc. where we assign some prediction to each word
2. But for a specific use case: discrete outputs corresponding to positions in the input sequence
3. Still based on standard LSTMs but with attention!

### Motivation?
Want to solve the 2-D convex hull problem using "learning" (data-driven)

1. Use LSTMs!
	1. Pass the coordinates of each vertex to the network followed by an <EOS> token.
	2. Using the final hidden state of the network, start producing output tokens

	PROBLEM 1: Need to know exactly how many classes (points) to classify amongst

	PROBLEM 2: LSTMs seem to be sensitive to the order of the inputs

	PROBLEM 3: LSTMs seem to perform poorly in long seqeunces


2. Use attention!
	1. Instead of relying on a fixed size "context" vector (the final hidden state of the LSTM), calculate context dynamically
	2. During output generation, calculate an "alignment" over the input hidden states:
		How much should my present output depend on the hidden state (i)?
	3. Calculate context by a weighted sum over the input hidden states:
		More important the input token for this output, more it's contribution to the output

	SOLVES PROBLEM 2 and PROBLEM 3 of LSTMs. However, we still need to know the number of classes to classify amongst (PROBLEM 3)

3. What is attention doing?
	1. Gives the highest weight to the input token which is most important for this output token
	2. Turns out, the highest alignment probability corresponded to the desired output!

	Insight: why not directly use this distribution?

### Proposed solution: Pointer networks
1. Calculate the alignment probabilities just like in vanilla soft-attention models
2. During training - this alignment is your output - just calculate the NLL loss!
3. For calculating the next hidden state with "context" - ?? (not specified clearly) - I think that it is the same as in soft-attention
4. During inference, take the argmax of the probs to get the prediction. Then, feed it back to the network.
    In practice, do a k-beam search instead. Also, they applied additional problem-specific constraints to get "valid" outputs (bias!)

Solves PROBLEM 1 as well!


### Major contributions
1. Allow for variable length dictionaries
2. Show that the model generalizes to sequences of length greater than the training data
3. Data-driven solutions to combinatorial problems that are computationally intractable

