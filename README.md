# deep-learning-challenge

#### By Karoly Burgyan

# Sources
<ol>
  <li>Dataset provided by IRS. Tax Exempt Organization Search Bulk Data Downloads. https://www.irs.gov/Links to an external site.</li>
  <li>ChatGPT https://chat.openai.com/</li>
  <li>Shayla Badeaux. Suggests not excluding 'NAME' column.</li>
</ol>

# Overview
This project was tasked with being able to predict, with at least an accuracy of 75%, which ventures would have the 'best chance of success' if given funding by the nonprofit foundation Alphabet Soup. <br>
Deep learning with neural networks were used to create a prediction model that tried to maximize accuracy in predicting for 'best chance of success'.

# Results

## Data Preprocessing
<ul>
<li>What variable(s) are the target(s) for your model?</li>The target for the model was:
<ul>
<li>IS_SUCCESSFUL—'Was the money used effectively'</li>
</ul>
<li>What variable(s) are the features for your model?</li>
The features for the model were:
<ul>
<li>APPLICATION_TYPE—'Alphabet Soup application type'</li>
<li>AFFILIATION—'Affiliated sector of industry'</li>
<li>CLASSIFICATION—'Government organization classification'</li>
<li>USE_CASE—'Use case for funding'</li>
<li>ORGANIZATION—'Organization type'</li>
<li>STATUS—'Active status'</li>
<li>INCOME_AMT—'Income classification'</li>
<li>SPECIAL_CONSIDERATIONS—'Special considerations for application'</li>
<li>ASK_AMT—'Funding amount requested'</li>
<li>NAME—'Identification column'</li>
</ul>
<li>What variable(s) should be removed from the input data because they are neither targets nor features?</li>
<ul>
<li>EIN—'Identification column'</li>
</ul>
</ul>

## Compiling, Training, and Evaluating the Model

<ul>
<li>How many neurons, layers, and activation functions did you select for your neural network model, and why?</li>
With the help of keras_tuner.Hyperband, the model chosen was the model that it found to have the highest accuracy when varying the number of layers, neurons, and activation functions. <br>The specs for the model chosen were as follows:
<ul>
<li>number of layers (excluding the output layer) -- 1</li>
<li>number of neurons in each layer (starting from the input layer)-- 130<sup>1<sup></li>
<li>activation function for each layer (starting from the input layer (excluding the output layer which used 'sigmoid')) -- 'relu'</li>
<li>learning rate -- 0.00044</li>
<li>optimizer -- 'adam'</li>
<li>output activation function -- 'sigmoid'</li>
<li>buckets -- 70 buckets (61 for 'NAME', 6 for 'CLASSIFICATION', and 3 for 'APPLICATION_TYPE')</li>
    <img src='./images/buckets_name.png'>
    <img src='./images/buckets_classification.png'>
    <img src='./images/buckets_application_type.png'><br><br>
<li>outlier limit -- 8 z-score threshold</li>
    <img src='./images/most_accurate_model_specs.png'><br>
</ul><br>
<li>Were you able to achieve the target model performance?</li>
Yes, the model had an accuracy of 96.35% which was 21.35% above the 75% target.
    <img src='./images/final_result_evaluation_accuracy.png'><br><br>
<li>What steps did you take in your attempts to increase model performance?</li>
<ul>
    <li>epochs -- the number of epochs were varied from 1 to 100</li>
    <li>layers -- (including input layer but excluding output layer) were varied from 1 to 11</li>
    <li>neurons per layer -- were varied from 2 to 2 X the number of features</li>
    <li>number of features -- were varied from 43 to 116</li>
    <li>activation functions -- were varied between 'relu', 'leaky_relu', and 'tanh' (for all layers except output layer which used 'sigmoid')</li>
    <li>bucket size -- varied the number of values that would be converted into 'other' from 0 to 63</li>
    <li>number of bucket -- varied from 0 to 100+</li>
    <li>removed outliers -- varied from a z-score limit of 1 to 35<sup>2</sup></li>
    <li>learning rate -- varied from 0.0001 to 0.01 for an 'adam' optimizer</li>

</ul>
</ul>


<sup>1</sup><sub style='font-size: 10;'> Doesn't include the 1 neuron in the output layer.</sub>

<sup>2</sup><sub style='font-size: 10;'> Note that these variations provide the backbone of a massive amount of potential permutations if the variations were done simultaneously and exhaustively. However, this task would take far more time and resources than is currently available.</sub>

# Summary

The model that was found had an accuracy of 96.35% which was above of the 75% accuracy by 21.35%. This model had 1 layer, a total of 130 neurons across that single layer<sup>1</sup>, and 2 different activation functions 'relu' and 'sigmoid'. It was tested on an initial dataset with over 34,000 datapoints. It would be very helpful in predicting successful ventures for the Alphabet Soup Charity to invest in.

<sup>1</sup><sub style='font-size: 10;'> Doesn't include the 1 neuron in the output layer. (repeated from above)</sub>


## Alternative Solution

An alternative model could possibly be found with more accuracy if more time and funding were available to vary the different parameters simultaneously and exhaustively. This would require vastly more processing power and energy if taken to the limit of trying every configuration simultaneously that was tried individually.