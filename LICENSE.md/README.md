# Teach your device in "One Go"
by Tejaswini Kancharla, December, 03, 2018

Introduction:
Language is the tool to express and there are a lot of languages in this world. When a person learns a different language all he would do is mapping i.e associating the new word to the words he already knows.Building upon this idea I wonder can we have a system that learns in "one go", in precise with one time teaching as computers can never forget on their own. May be not the entire language but atleast commands that will be used to perform tasks.

This project builds a small program in which you can use custom commands to perform a task rather than using the standard commands. It is a calculator that just perform addition and multiplication, I am using these two operations becuase of their commutative property which makes my project less complex while dealing with order of numbers.

I am very much interested in this project because it could save a lot of time. To illustrate this if you want to open the jupyter notebook in your laptop you should always open the command prompt and give it a series of commands but using this technique you can replace all those commands with a single command of your choice.

This technique also makes the lives of visually impaired people much better. As they can train their devices as they want.

At the very beginning of Computer era, people used to interact with computers in 0 and 1 language and then there came programming languages like C, Python etc. At present natural language with predefined commands and now, why not the commands of our own choice?

Methods
In a nut-shell what all I have done is created a basic calculator which just performs addition and multiplication when you use commands "add" and "mul" respectively. These basic commands will be stored in a text file called "keywords" in the form of dictionary like {"add":"+","mul":"*"}. But when you use other command like "sum" it would guesses the closest command from the commands it knows (basic "add" and "mul" along with any other pre-trained words) and performs the operation of that command. It then asks the user whether it is the output he is expecting, if the user responds "Y"(yes) then it learns this new command and associates it with the operation it just performed otherwise also it learns this new command but associates it the operation it did not perform (it is easy as we just have two operations). Let us have a deep look into how it is implemented.

I divide the project into three parts:

Command or keyword extraction
Guessing the closest keyword
Executing the operation associated with the keyword
Managing the memory
The tools I used in this project are nltk, numpy and json files.

Command or Keyword Extraction:
In order to give the perfect response to the user, the program must understand the input well. In our case the main tasks involved in understanding the input is to know what is the major keyword(that describes operation) and the numbers on which the operation has to be performed.

To complete these two tasks I used nltk to process the command and extract the useful information from it in the following steps:

Taking the input command from the user
Used nltk to tokenize the command sentence into words and tagged them according to their parts of speech using pos_tag() method of nltk.
I extracted the numericals(tagged as CD-Cardinal Digit) from the sentence and stored them in a list called num and converted this list into integer float.
Then I eliminated all the prepositions and conjunctions from the sentence which were tagged as "CC" and "IN".
Now the command variable contains only the actual command the user wants to use to perform the task.
I pass this command variable and num list to a function called execute() (which executes the command).
Guessing the closest Keyword:
After extracting the keyword we should identify the operation associated with that particular keyword. In order to do that we should first check whether that particular keyword is present in the list of keywords that the program already knows if not we should identify the closest keyword to it. This identification is done by calculating the "edit distance" between the extracted keyword and all the list of keywords the program knows, then the smallest edit distance gives the closest keyword. Edit distance is the number of changes need to be made to make one word equal to other word. I used inbuilt "edit_distance" function from nltk.

Executing the operation associated with the keyword:
I used numpy to perform the operation. As I stored the numbers in a list, I converted it into a numpy array and then used np.sum and np.prod to perform addition and multiplication. I can also use traditional way to perform the operation but doing so may be hectic when there are more than two numbers in the num list.

Managing Memory:
If the keyword is not the exact keyord from the list that is if it is the closest keyword to the one in list then after executing the operation associated with the keyword the program asks the user whether it is right. If the user replies "yes" then the program learns this new keyword and associates it with the operation it has just performed. If the user replies "no" then the program still learns the keyword but it associates it with the other operation.

Json Files:
I should store the new commands and their operations in a file in order to

execute(command, num) Function:
This function contains a dictionary called operations which contains just two keys '+' and '*' whose values will calculate sum of all numbers in num list and multiply all numbers in num list respectively.
Steps I took. Resources I used, such as code from the class, on-line resources, research articles, books [Goodfellow, et al., 2016], ....
