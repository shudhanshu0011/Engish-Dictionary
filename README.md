In Python, a dictionary is an “unordered collection of data values, used to store data values like a map” (source). It works in a similar manner just like the real world dictionary where all the keys are unique and of immutable data type.

In this guide we will be creating an interactive English dictionary which will not only allow the user to type in words to get meaning but also provide word suggestions in the case of a misspelling.

Python Dictionary Workflow
This particular article is going to be divided into two parts, for the first part we are going to develop a terminal based application and later we will move into developing an interactive GUI app.

Despite the steps taken, that is either GUI based or Terminal based our dictionary will work the same performing the same operations, that is:

The first step, the JSON file will be loaded into python.
Get user input
Cross check the meaning of the word from the JSON file
Creating Dictionary App
Terminal SetUp
In order for us to create our interactive dictionary and use it in the terminal, we will need:

A .py file – which will contain our code.
A data file – which is a JSON file that contains vocabularies that will be checked against giving meaning of words asked for.
difflib – help us compare various sequences and give us a list of words which are close to what the user intended to search for. 
Now that we have all the necessary files and modules we will need, let’s get started by developing our terminal based application.

Use this link to download the JSON file.

The first step will be for us importing the libraries that we will be using, and that is done as shown below.

import json
from difflib import get_close_matches
Next we load up the JSON file.

data = json.loads(open('data.json').read())
At this point now we can go ahead and write our main function which will contain the code shown below. Just a simple breakdown of the main function is:

We have defined a function: definition.
Converted all user input into lowercase to match words in JSON file.
If statement to check if words given exist, suggest possible words, and return an error if word does not exist.
def definition(name):
    name = name.lower()
    if name in data:
        return data[name]
    elif len(get_close_matches(name, data.keys())) > 0:      
        check = input("Did you mean %s instead? Enter Y if yes, otherwise N to exit: " %
                      get_close_matches(name, data.keys())[0])
        if check == "Y":
            return data[get_close_matches(name, data.keys())[0]]
        elif check == "N":
            return "The word doesn't exist. Please double check it."
        else:
            return "We didn't understand your entry."
    else:
        return "Sorry, this word is not an English word. Please double check your spelling."
Next, we now pass in the method that will take in the user input and check it against the set of words passed in the  JSON file.

word = input('Enter a name: ')
The last step is to add an output format. We need to get our answers arranged in an easier manner to read, and in order to achieve that we make use of the if statement and for loop. Which will list all meanings in a separate line in the terminal.

To achieve that, we make use of the code below.

output = definition(word)
if type(output) == list:  
    for item in output:
        print(item)
else:
    print(output)
Now let’s go ahead and test out our program by running it on different instances.

If you check an English word, for example the word “program” the output will be as shown below.


What if we happen to misspell a word, will we be able to get correct suggestions? For example let’s take an instance where we want to get the meaning of the word rain but we misspell it by typing rrainn, will we get the correct suggestion?


Similarly if we happen to type a word that is not in the english dictionary, we will get an error message saying the word is not an english word, for example:


From the above code output samples, we have been able to create an interactive dictionary operated from the terminal and we are able to get words meaning and also correctly tell if a word is misspelled or does not exist in the english dictionary.

Now let’s go ahead and create a GUI based dictionary.

GUI based Dictionary 
In this particular section, we will do things a little bit differently. Since we will need an interface we will interact with we are going to use different modules compared to our terminal app.

In this case apart from having a .py file, we are going to make use of:

PyDictionary – A Python module that will help us get meanings, synonyms and antonyms of words.
Tkinter – A python framework that will enable us to create GUI elements usings its widgets found in the Tk toolkit.
