# Markov-chain
You are given a starting state start, a list of transition probabilities for a Markov chain, and a number of steps num_steps. Run the Markov chain starting from start for num_steps and compute the number of times we visited each state.

#include <bits/stdc++.h> 
using namespace std; 
  
// Macro for vector of pair to store 
// each node with edge 
#define vp vector<pair<int, float> > 
  
// Function to calculate the 
// probability of reaching F 
// at time T after starting 
// from S 
float findProbability(vector<vp>& G, int N, 
                      int F, int S, int T) 
{ 
    // Declaring the DP table 
    vector<vector<float> > P(N + 1, vector<float>(T + 1, 0)); 
  
    // Probability of being at S 
    // at t = 0 is 1.0 
    P[S][0] = 1.0; 
  
    // Filling the DP table 
    // in bottom-up manner 
    for (int i = 1; i <= T; ++i) 
        for (int j = 1; j <= N; ++j) 
            for (auto k : G[j]) 
                P[j][i] += k.second * P[k.first][i - 1]; 
  
    return P[F][T]; 
} 
  
// Driver code 
int main() 
{ 
    // Adjacency list 
    vector<vp> G(7); 
  
    // Building the graph 
    // The edges have been stored in the row 
    // corresponding to their end-point 
    G[1] = vp({ { 2, 0.09 } }); 
    G[2] = vp({ { 1, 0.23 }, { 6, 0.62 } }); 
    G[3] = vp({ { 2, 0.06 } }); 
    G[4] = vp({ { 1, 0.77 }, { 3, 0.63 } }); 
    G[5] = vp({ { 4, 0.65 }, { 6, 0.38 } }); 
    G[6] = vp({ { 2, 0.85 }, { 3, 0.37 }, { 4, 0.35 }, { 5, 1.0 } }); 
  
    // N is the number of states 
    int N = 6; 
  
    int S = 4, F = 2, T = 100; 
  
    cout << "The probability of reaching " << F 
         << " at time " << T << " \nafter starting from "
         << S << " is " << findProbability(G, N, F, S, T); 
  
    return 0; 
} 
