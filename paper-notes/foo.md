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
