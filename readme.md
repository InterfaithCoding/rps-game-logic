The Game Logic
==============

This week we're going to write the logic for our 'Rock, Paper, Scissors' game. At the moment, we have a mockup of our website, but when you click on our icons, nothing really happens. We have to write the logic, so that the programme knows what to do when the player has made their selection, can determine who has won the game, and can declare the winner. 

To keep it simple to deploy our app to the web, we are going to use JavaScript. JavaScript is a unique language in that it can be used for both back-end logic and front-end user interaction, making it one of the web's most widely used languages. We could also have decided to write our game logic in a language such as Python, but we would need a web framework like Django to deploy our app to the web. This is beyond the scope of the course, but if you are interested, a [quick Google search](https://www.djangoproject.com/) should tell you about Django and web frameworks.

The main programming concepts that we need to build the game logic, such as declaring variables, conditional logic and if/else statements, are all concepts that we encountered when learning Python. The main differences are going to be in the syntax, so pay close attention.

###The Rules of the Game

Rock paper scissors is a classic 2 player game. Each player chooses either rock, paper or scissors. The possible outcomes:

Rock destroys scissors.
Scissors cut paper.
Paper covers rock.

We'll add in lizard and spock soon - but let's get an initial version of our game working first, and then we'll add more complexity to it later. 

Let's think about how our game is going to work in plain English, before we even start thinking about how we are going to code it. We will call this our 'prep code'. Discuss this with your partner what our prep code should look like before reading the next section. 

###Prep code

Our code will break the game into 4 sections:

1. Firstly, our player makes a choice
2. Then the computer needs to choose
3. We need to compare the choices to determine a winner
4. We need to declare the winner

###Writing the code

Now we have a solid idea of how our programme is going to work, let's think about the actual code we want to write to achieve this.

####1. We start by first asking the user for their choice. 

In the initial version of our game logic, this is going to be a console application i.e. we are going to get the user choice, by simply asking them for it. Remember how we used 'input' in Python to get user input? On our final website though, we will get their choice from the icon that they click. We will learn how we can do this using JavaScript next week, when we finally tie the front and back-end of our website together. 

We need to declare a variable called ```userChoice```

#####How do we create variables in JavaScript?

We use the keyword ```var``` followed by the name that we would like to call our variable. We then assign it the value that we want to store in our variable. At the end of each statement in JavaScript, we need to put a semi-colon - this is similar to putting a full-stop at the end of an English sentence. 

E.g. to declare a variable that stores the string "Hello"
```
var nameOfVariable = "Hello";
```
To get user input in JavaScript we use the inbuilt JavaScript function ```prompt()```

So our variable to get and save our player's choice might look something like this:

```var userChoice = prompt("Do you choose rock, paper or scissors?");```

####2. We next want to get our computer's choice. 

We want our computer to make a decision randomly. Fortunately for us, JavaScript has an inbuilt random function. 

If we declare a variable and make it equal to ```Math.random()```, that variable will equal a number between 0 and 1.

But we need to translate our random number between 0 and 1 in to a random choice of rock, paper or scissors. How should we go about implementing this?

If our random number is between 0 and 0.33, let's say that the computer picks rock, if it is between 0.34 and 0.67, the computer picks paper, and if it is greater than 0.67 the computer picks scissors. Let's use if/else if/if statement to tell our computer this logic.

```
var computerChoice = Math.random();

if (computerChoice <= 0.33) {
    computerChoice = "rock"
} else if (computerChoice <= 0.67) {
    computerChoice = "paper"
} else {
    computerChoice = "scissors"
}
```
We are changing the value of computerChoice based on the rules that we stated above. You do not have to use the keyword ```var``` when changing the value of a variable that already exists.

####3. We now have a user choice and a computer choice. We need to create a function to compare these two values, and to decide on a winner based on that comparison. 

First let's explore what functions are, and how we can write them in JavaScript

#####Functions in JavaScript

Programming is similar to baking cakes. Imagine you are trying to teach your friend how to bake different types of cakes.

Each cake make require different ingredients (ie. inputs), but the 'bake' instructions are always the same. E.g.

1. Pre-heat the oven
2. Mix all the ingredients in a bowl
3. Put contents into oven for 30 mins

The output will be a different cake each time, and the instructions might vary slightly. For example, we might want to cook different cakes at different temperatures.  

Bakers (and programmers!) are lazy and don't want to have to write out exactly the same 'bake' instructions every time we want to tell someone how to bake a cake. They would prefer just to say 'bake' and then anyone would know to execute those three steps. This is exactly what a function is.

A function takes in inputs, does something with them, and produces an output.

#####So how do we write functions in JavaScript?

We first need to declare function using ```var```, and then give it a name e.g. ```bakeCake```. The name should begin with a lowercase letter and the convention is to use lowerCamelCase where each word (except the first) begins with a capital letter.
Then we use the ```function``` keyword to tell the computer that you are making a function.

E.g. 
```
var bakeCake = function(typeOfCake) {
	if typeOfCake == 'chocolateCake' {
		temperature = 180;
	} else {
		temperature = 220;
	}
}
```
The code in the brackets is called a parameter. It's a placeholder word that we give a specific value when we call the function. For example, if we wrote a bakeCake function that gives us different baking temperatures based on what cake we were baking, we could have typeOfCake as a parameter. If we call the function using the parameter (chocolateCake) it would give us a different temperature to if we passed in a (spongeCake). 

We then we write our block of reusable code between the curly braces { }. Every line of code in this block must end with a semi-colon.

To use the function, we call the function by just typing the function's name, and putting a parameter value inside the brackets after it. The computer will run the reusable code with the specific parameter value substituted into the code. For example, if we want to bake a chocolate cake, we could call the function like so:

```
bakeCake(chocolateCake)
```

####Compare function

Now we know a bit about functions in JavaScript we can write our 'compare' function. 

Our function is going to have to take two parameters as input - the two choices that have been made - and will return the winning choice to us. The winning choice is our output. 

Let's figure out all the various outcomes of our comparison. One outcome is that the choice the user makes is equal to the choice the computer makes.
```
var compare = function(choice1, choice2) {
    if(choice1 == choice2) {
        return "The result is a tie!";
    }
};
```
What if choice1 is "rock"? Given choice1 is "rock",

a. if choice2 == "scissors", then "rock" wins.
b. if choice2 == "paper", then "paper" wins.

How do we structure this? It's a bit different from what we have already seen. We will first have an ```if``` statement. And then the code inside that if statement will be another if statement!
```
var compare = function(choice1, choice2) {
    if(choice1 == choice2) {
        return "The result is a tie!";
    }
    else if(choice1 == "rock") {
        if(choice2 == "scissors") {
            return "rock wins";
        }
        else {
            return "paper wins";
        }
    }
};
```
Now what if choice1 is "paper"? Given choice1 is "paper",

a. if choice2 == "rock", then "paper" wins.
b. if choice2 == "scissors", then "scissors" wins.
```
 else if(choice1 == "paper") {
        if(choice2 == "rock") {
            return "paper wins";
        }
        else {
            return "scissors wins";
        }
    }

 }
```
 Lastly, what if choice1 is "scissors"? Given choice1 is "scissors",

a. if choice2 == "rock", then "rock" wins.
b. if choice2 == "paper", then "scissors" wins.
```
var compare = function(choice1, choice2) {
    if(choice1 === choice2) {
        return "The result is a tie!";
    }
    else if(choice1 == "rock") {
        if(choice2 == "scissors") {
            return "rock wins";
        }
        else {
            return "paper wins";
        }
    }
    else if(choice1 == "paper") {
        if(choice2 == "rock") {
            return "paper wins";
        }
        else {
            return "scissors wins";
        }
    }
    else if(choice1 =="scissors") {
        if(choice2 == "rock") {
            return "rock wins";
        }
        else {
            return "scissors wins";
        }
    }
};

compare(userChoice, computerChoice); //here we call the function
```

This is what our final compare function looks like. 

There is much to improve about this function. Think about what other pieces of information would be useful for our game or players to know? If you discuss with you partner, we can try and implement these features in our final version next week.