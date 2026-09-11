# Machine-Learning
ML is the process of **training** a piece of software, called a **model**, to make useful **predictions** or generate content (like text, images, audio, or video) from data. It differs from classical approaching in predictions as it identifies key mathematical patterns and relationships using vast amount of historical data, whereas classical approaching rely on creating physical simulations with all variables that are incredibly compute intensive
### Key Words
1. Data - Data can be numbers, images, anything, It is the driving force of ML, we tore data in datasets
2. Dataset - Datasets are made of examples of data that contain **features** and a **label**. Features are the values that a supervised model uses to predict the label. The label is the "answer," or the value we want the model to predict. Good datasets are both **large and highly diverse.**
3. Model - is the complex collection of numbers that define the mathematical relationship from input feature patterns to output label values. The model discovers these patterns through training.
4. Training - Is the process of giving model dataset of labeled examples, and let the model run cases of prediction. Predictions are corrected by quantifying the difference between the expected value and the output value as loss, which the model tries to gradually reduce. Simply, the model learns the mathematical relationship between the features and the label so that it can make the best predictions on unseen data.
## Types of ML Models based on their functionality
## 1. Supervised learning
Supervise learning is when the model is trained on data that has it's features already been **labelled** by a human. The model simply learns the pattern and begins predicting the output (labels) from the input (unlabeled examples). There are two major types of supervised learning models:
### i) Linear Regression:
A regression model predicts a **numeric value**. For example, a weather model that predicts the amount of rain, in inches or millimeters, is a regression model. In a Linear Regression Model, the target values (labels) are numerical values.

 **$x^{(i)}, y^{(i)}$ means the model input and labeled output respectively, at $i^{th}$ index in the dataset, where $\hat{y}$ would mean the model output.** 
 
 The model is just a mathematical function with a relationship between the input and output.

$f_{w,b}(x^{(i)})$ | The result of the model evaluation at $x^{(i)}$ parameterized by $w,b$: $f_{w,b}(x^{(i)}) = wx^{(i)}+b$. Where $w$ = weight, $b$ = bias of the model.
#### Cost Function (J)
  Takes the prediction by the model $\hat{y}$  and compares it with the the expected output $y$ by subtracting them. This measure is called the **error = $(\hat{y}-y)^2$. 
  
  $1/2m\sum_{i=1}^{m}(\hat{y}-y)^2$ 
  
  This is the entire cost function used commonly in linear regression models, every model may have a different cost function based on the needs. Here m is the number of total examples in the dataset, this is called square-error cost function.
  
  The purpose of the model is to find such values of $w$ and $b$ such that the cost function reduces. Commonly we can ignore $b$ and then the **Cost Function (J) becomes a function of $w$ (the weight)**, and now we can simply focus on finding the value of $w$ for which the Cost Function in minimal.
### ii) Classification:
Classification models output a value that states whether or not something belongs to a particular category. Ex: classification models are used to predict if an email is spam or if a photo contains a cat.

They are further of two major types:
- **Binary Classification -** Outputs value from a class that only **contains two values**, like **`rain`** or **`no-rain`**.
- **Multiclass Classification -**  output a value from a class that contains more than two values, for example, a model that can output either **`rain`**, **`hail`**, **`snow`**, or **`sleet`**.
## 2. Unsupervised learning
Unsupervised learning aims to identify meaningful patterns in any given dataset without output labels being provided. They rely on a technique called **clustering** where similar data is organized into groups. **This is particularly useful when humans do not know the patterns in the data, and the model can help identify them.**
### Clustering 
differs from classification as these categories aren’t defined by the user. Common examples of where clustering is used are: google news, DNA microarray. Other examples of unsupervised learning are anomaly detection and dimensionality reduction.
## 3. Reinforcement learning
These models make predicts by being rewarded or penalized based on their actions performed within an environment.
## 4. Generative AI
A class of models that creates content from user inputs, it can summarize essays and is not restricted by the type of input or output. ex: text-to-image, text-to-text
# Transformers
