# Restaurant Bot

This is an implementation of a [RASA](https://rasa.com/) based chatbot that integrates with [Zomato API](https://developers.zomato.com/) 
to fetch restaurant information and serve you a list of restaurants for you to consider based on your selected Cuisine, Budget & City. 
Additionally, the list of restaurants is also emailed to you with the top restaurants for your selected criteria.

* NOTE: This implementation currently only works in Tier 1 & Tier 2 cities in India. List of Tier 1 & Tier 2 cities is 
available [here](https://en.wikipedia.org/wiki/Classification_of_Indian_cities).

## Pre-requisites
Open a terminal in Administrator mode on windows or use 'sudo su' in Unix to install the following packages in a 
virtual environment.

All dependencies listed in deps.txt file. 


Model size was over 90mb for both NLU trained models and the NLU implementation model so they have not been provided.
Once implementation is done the models will be stored in the _models_ folder
### Installation

### Conda

For installation and package management we use [Anaconda](https://docs.anaconda.com/anaconda/install/)


```python
conda create -n rasa
```
### RASA

Refer to official [installation guide](https://rasa.com/docs/rasa/user-guide/installation/) to install RASA

```python
pip install rasa==2.0.0a2
```
### Spacy

1. Package Installation

   ```python
    pip install rasa[spacy]==2.0.0a2
   ```

2. Model Installation

   ```python
   python -m spacy download en_core_web_md
   ```

3. Create custom shortcut link to Spacy model

   ```python
   python -m spacy link en_core_web_md en
   ```

## Repo Information

This repo contains training data and script files necessary to compile and execute this restaurant chatbot. It comprises of the following files:

### Data Files

- **data/nlu.yml** : contains training examples for the NLU model  
- **data/stories.yml** : contains training stories for the Core model  

### Script Files

- **zomato** : contains Zomato API integration code
  - **zomato_api.py** : contains functions to consume common Zomato APIs like fetch location details, type of cuisines, search for restaurants, etc
  - **zomato_test.py** : contains 3 test functions for Zomato API - location details, cuisine details and restaurant search
- **actions.py** : contains the following custom actions 
  - search restaurant
  - validate location
  - validate cuisine
  - send email



### Config Files

- **config.yml** contains model configuration and custom policy
- **credentials.yml** contains authentication token to connect with channels like slack
- **domain.yml** defines chatbot domain like entities, actions, templates, slots  
- **endpoints.yml** contains the webhook configuration for custom action

## Usages

- Train the NLU model

  ```python
    rasa train nlu
  ```

  This will generate _nlu-datetimestamp.tar.gz_ inside **models** folder and start an interactive shell

- Open the ```actions.py``` file and insert insert the **ZOMATO API** key in this script in the ```user_key``` section before starting RASA server from [here](https://drive.google.com/file/d/1z9a-VShW7K619B6QEm5ezAwrTgtF15fM/view?usp=sharing), your email id & password in the ```sender_email & sender_password``` at  the bottom of the file
If the user key isn't available, use the same as provided in the Rasa_basic_folder example.
- Run RASA action server in a new terminal/command line. Make sure you start the cmd line in Administrator mode

  ```python
  rasa run actions
  ```
  
- Train RASA NLU model
  
  ```python
  rasa train
  ```

- Starts an interactive session with restaurant chatbot

  ```python
  rasa shell
  ```



## Authors:

Naveen Sharma & Nirbhay Tandon for UpGrad NLU Rasa Chatbot Assignment