
ML is the process of **training** a piece of software, called a **model**, to make useful **predictions** or generate content (like text, images, audio, or video) from data. It differs from classical approaching in predictions as it identifies key mathematical patterns and relationships using vast amount of historical data, whereas classical approaching rely on creating physical simulations with all variables that are incredibly compute intensive

## Key Words

Data - Data can be numbers, images, anything, It is the driving force of ML, we tore data in datasets

Dataset -

Model - is the complex collection of numbers that define the mathematical relationship from input feature patterns to output label values. The model discovers these patterns through training.

Training -

## Types of ML Models based on their functionality

### 1. Supervised learning

Supervise learning is when the model is trained on data that has already been _**labelled** with correct and incorrect answers_ by a human. The model simply learns the pattern ad begins predicting the output from the input. There are two major types of supervised learning models:

#### **i) Regression:**

A regression model predicts a **numeric value**. For example, a weather model that predicts the amount of rain, in inches or millimeters, is a regression model.

#### **ii) Classification:**

Classification models output a value that states whether or not something belongs to a particular category. Ex: classification models are used to predict if an email is spam or if a photo contains a cat.

They are further of two major types:

- **Binary Classification -** Outputs value from a class that only ****contains two values, like **`rain`** or **`no-rain`**.
- **Multiclass Classification -**  output a value from a class that contains more than two values, for example, a model that can output either **`rain`**, **`hail`**, **`snow`**, or **`sleet`**.

### 2. Unsupervised learning

Unsupervised learning aims to identify meaningful patterns in any given dataset without output labels being provided. They rely on a technique called **clustering** where similar data is organized into groups. **This is particularly useful when humans do not know the patterns in the data, and the model can help identify them.**

Clustering differs from classification as these categories aren’t defined by the user. Common examples of where clustering is used are: google news, DNA microarray.

Other examples of unsupervised learning are anomly detection and dimensionality redution.

### 3. Reinforcement learning

These models make predicts by being rewarded or penalized based on their actions performed within an environment.

### 4. Generative AI

A class of models that creates content from user inputs, it can summarize essays and is not restrited by the type of input or output. eg: text-to-image, text-to-text