# CDC-OIICS
Repo for the CSC Occupational Injury and Illness Classification System (OIICS) topcoder competition

I signed up for the "CDC Text Classification Marathon"

This is the information from the challenge:

**Overview**
Every day, work-related injury records are generated. In order to alleviate the human effort expended with coding such records, the Centers for Disease Control and Prevention (CDC) National Institute for Occupational Safety and Health (NIOSH), in close partnership with the Laboratory for Innovation Science at Harvard (LISH), is interested in improving their NLP/ML model to automatically read injury records and classify them according to the Occupational Injury and Illness Classification System (OIICS).

**Objective**
The task is a well-defined classification problem. The programming languages are strictly limited to Python and R.

The input training file is a spreadsheet, with 4 columns (text, sex, age, and event). This CSV file contains a header.

**text** This column describes the raw injury description text data.

**sex** This is a categorical variable, describing the sex of the related person.

**age** This is a positive integer variable, describing the age of the related person.

**event** This is the target variable, specifying the OIICS label to be classified. There are 48 unique labels in total.
 
You are asked to build a model based on the above training data. And your model will need to make predictions for the following test file.

 The test file is a spreadsheet, with only 3 columns (text, sex, and age). This CSV file contains a header. The format is the same as the training file, but the event column will be missing. Once your model is trained, it should be able to consume the test file and produce the prediction file by filling in the Event column. Specifically, your output will be a CSV file with all 4 columns, keeping the same order as the test file.

**Datasets**
There are 229,820 records in total. 

We have randomly sampled 153,956 of the records with the event column included as the training set. You are asked to use this training set to develop your model locally. The remaining 75,864 of the records are held out for the testing purpose. You can download the 3-column spreadsheet testing set here (The event column will be missing). In your submission, you will need to include all predictions for the records in the testing set, following the same order.
 
**Baseline**
The client has tried to build a model using BERT. It achieves an accuracy of around 87% based on their local testing. We will post the baseline codebase in the forum. Their model may help you identify potential avenues for improving the solution.

**Performance**
I was not able to meet the baseline. However, this was a very instructive experience for me. I was taking an NLP class when I signed up for this challenge, so I applied my learnings to this dataset.

After trying a basic fully-connected layer NN, I tried a bi-directional LSTM using GLoVE embedding and finally ended up building a BERT model. However, I ended up spending a lot of time looking at cleaning up the dataset.

Since the text is hospital admission records, there are a lot of medical/clinical abbreviations, and many of them are incorrect (typos) and hence I needed significant pre-processing to fix this. Note that BERT uses a wordpiece tokenizer, so the abbreviations (e.g. yom = year old male, lac=laceration) needed to be expanded so that the BERT tokenizer would be able to correctly find the embeddings.

I ended up with a best score of **84%**.
