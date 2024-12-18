![estimator](https://raw.githubusercontent.com/jjanbol/nsl_kdd/refs/heads/main/q4_2.png)

Following are the final hyper tuning parameters:

1. `lr = 0.001`
2. `batch_size = 205`
3. `N_epochs = 10`
4. `optimizer = torch.optim.Adam(mymodel_hyper.parameters(), lr = lr)`
5. NN structure
myMultiLayerPerceptron(

(sequential): Sequential(
  
    (0): Linear(in_features=113, out_features=55, bias=True)
    (1): ReLU()
    (2): Linear(in_features=55, out_features=20, bias=True)
    (3): ReLU()
    (4): Linear(in_features=20, out_features=10, bias=True)
    (5): ReLU()
    (6): Linear(in_features=10, out_features=7, bias=True)
    (7): ReLU()
    (8): Linear(in_features=7, out_features=5, bias=True)))


The hypertuning process was mostly based on Trial and Error. 

Initially learning rate of 0.0001 and even smaller was implemented, resulting in slow convergence and not reaching good accuracy on both training and validation dataset. `lr=0.001` seemed to be the sweet spot for fast convergence.

For `batch_size`, different values were explored. Although a larger `batch_size` of 300 made the training faster, it led to lower validation accuracy. Reducing it to 205 helped accuracy reach close to 89%

Testing with more than 10 epochs revealed diminishing returns. The model typically converged within the first 10 epochs, and subsequent epochs did not yield significant improvements. To optimize computational efficiency, I decided to maintain the `N_epochs` count at 10.

The most substantial improvememnt came from the neural network structure. My initial NN model with 3 layers reached a maximum validation accuracy of 80%. Although increasing the depth introduced higher risk of overfitting to the training data, 5 layers NN structure resulted in improved performance, raising validation accuracy to 89%.

For optimizer Adam was chosen as it allows faster convergence when compared to the SGD. When using lower learning rate, the convergence was quite slow with SGD.


Overall results:
| Model                   | Train Accuracy | Validate Accuracy | Train Loss           | Validate Loss       | Notes              |
|-------------------------|----------------|-------------------|----------------------|---------------------|--------------------|
| Neural Network (No Tuning) | 97.42%         | 81.46%            | 0.1029256209731102  | 1.0464439392089844  | Without Hypertuning |
| Neural Network (Tuned) | 99.48%         | 89.31%            | 0.017658818513154984 | 1.8183221817016602  | With Hypertuning   |
