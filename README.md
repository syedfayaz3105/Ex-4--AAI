<H3>Name: FARHANA H</H3>
<H3>Register No: 212223230057</H3>
<H3>Experiment: 4</H3>
<H3>Date:12.05.26 </H3>
<H1 ALIGN =CENTER> Implementation of Hidden Markov Model</H1>

## Aim: 
Construct a Python code to find the sequence of hidden states by the known sequence of observances using Hidden Markov Model. Consider two hidden states Sunny and Rainy with observable states happy and sad

## Algorithm:
<b>Step 1:</b> Define the transition matrix, which specifies the probability of transitioning from  one hidden state to another

<b>Step 2:</b> Define the emission matrix, which specifies the probability of observing each possible observation given each hidden state

<b>Step 3:</b> Define the initial probabilities, which specify the probability of starting in each possible hidden state

<b>Step 4:</b> Define the observed sequence, which is the sequence of observations need to  be analyzed

<b>Step 5:</b> Initialize the alpha matrix with zeros, where each row represents a time step and each column represents a possible hidden state

<b>Step 6:</b> Calculate the first row of the alpha matrix by multiplying the initial  probabilities by the emission probabilities for the first observation

<b>Step 7:</b> Loop through the rest of the observed sequence and calculate the rest of the alpha matrix by multiplying the emission probabilities by the sum of the product of the previous row of the alpha matrix and the corresponding row of the transition matrix

<b>Step 8:</b> Calculate the probability of the observed sequence by summing the last row of the alpha matrix

<b>Step 9:</b> Find the most likely sequence of hidden states by selecting the hidden state with the highest probability at each time step based on the alpha matrix

## Program:
```python
import numpy as np

transition_matrix = np.array([[0.7,0.3],[0.4,0.6]])
initial_probabilities = np.array([0.5,0.5])
observed_sequence = np.array([1,1,1,0,0,1])
emisson_matrix = np.array([[0.1,0.9],[0.8,0.2]])

alpha=np.zeros((len(observed_sequence),len(initial_probabilities)))
alpha[0,:]=initial_probabilities*emisson_matrix[:,observed_sequence[0]]

for t in range(1,len(observed_sequence)):
  for j in range(len(initial_probabilities)):
    alpha[t,j]=emisson_matrix[j,observed_sequence[t]]*np.sum(alpha[t-1,:]*transition_matrix[:,j])
probability=np.sum(alpha[-1,:])
print("The probability of the observed sequence is:",probability)

most_likely_sequence=[]
for t in range(len(observed_sequence)):
  if(alpha[t,0] > alpha[t,1]):
    most_likely_sequence.append("sunny")
  else:
    most_likely_sequence.append('rainy')
print("The most likely sequence of weather states is:",most_likely_sequence)
```

## Output:
<img width="887" height="50" alt="image" src="https://github.com/user-attachments/assets/5daa00df-e6fa-4fe8-9d40-5d77ac71b888" />

## Result:
Thus, Hidden Markov Model is implemented using Python
