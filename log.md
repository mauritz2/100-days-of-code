# 100 Days Of Code - Log

### Day 0: October 1, 2022

**Today's Progress**: Added test cases for the determine winner function in Arboretum and added the graveyard class 

**Thoughts:** This was interesting: https://stackoverflow.com/questions/33533148/how-do-i-type-hint-a-method-with-the-type-of-the-enclosing-class
How to do type hints when you're type hinting the class itself. Tried the from __ future __ import annotations solution, but it threw an error.
Seems like it messed up how the Player class was being interpreted in an unexpected way. Would like to understand what __future__is better

**Project** https://github.com/mauritz2/arboretum

### Day 1: October 2, 2022

**Today's Progress**: Added the Game Manager to Arboretum and started implementing its logic

**Thoughts:** Realizing it's best to implement even very simple methods for classes, to reduce coupling.
E.g. I know the deck is a list of cards, so to get the top card I could do [-1]. But if I change it so that the top card is now [0],
or I change cards to be a dict I now have to change both the Deck class, AND where I referenced [-1]. So better that
the Deck class has a method called get_top_card() to abstract how it actually gets that card.

**Project** https://github.com/mauritz2/arboretum

### Day 2: October 3, 2022

**Today's Progress**: Finalized a first version of the complete Arboretum game logic

**Thoughts:** Feels good to put all the pieces together finally. There's more clean-up to be done (e.g. allowing for draws, refactoring,
making it more clear what paths scored points). But main thing would be to build a front-end for this logic that can be interacted with.
I'd probably turn it into a Flask app. TBD.

**Project** https://github.com/mauritz2/arboretum

### Day 3: October 4, 2022

**Today's Progress**: Took a first pass at turning Arboretum into a web app

**Thoughts:** Found a six-year-old Flask app that implemented Hearts that I'll use as a base for building Arboretum into a web app :-) https://github.com/rohanil/hearts
The original ambition was to make the cards draggable, but seems easier to start with just having a "Play" button per card that hide/show based on whose turn it is
Found out about Miniconda - it works well, I can manage envs there without having to install full Conda https://docs.conda.io/en/latest/miniconda.html

**Project** https://github.com/mauritz2/arboretum

### Day 4: October 5, 2022

**Today's Progress**: Updated the web app so that it can display a player's hand

**Thoughts:** Brushing up on some Bootstrap and CSS. To introduce bottom padding do "pb-x" where x is the bottom padding.

**Project** https://github.com/mauritz2/arboretum

### Day 5: October 6, 2022

**Today's Progress**: Continued on the web app - rendering the board and first pass at being able to choose a card and then play it to the board

**Learnings:**
* CSS cares about spaces .table : hover didn't work, but .table:hover works,
* Margin controls the space OUTSIDE an element, padding controls the space INSIDE an element. I always tend to use padding, but should be using more margin since that's most often what I need to change
* Fun Flask issue to troubleshoot: the web app wouldn't update. The issue was that PyCharm was running the main() which was also running Flask. Stopping that caused the app to start refreshing again.

**Project** https://github.com/mauritz2/arboretum

### Day 6: October 7, 2022

**Today's Progress**: Followed a tutorial on how to set up a simple API using Flask (https://auth0.com/blog/developing-restful-apis-with-python-and-flask/#-span-id--flask-on-docker----span--Dockerizing-Flask-Applications)

**Learnings:**
* The timeit Python module can be used to test performance on short snippets of code, e.g.: python -m timeit '"-".join(str(n) for n in range(100))'. This is cool. When I tried to time some code earlier both options executed too quickly to see the difference in the execution time, but timeit can execute it 1000s of times to spot the difference. 
* Windows doesn't have a wget or curl equivalent. But a Windows-version of Wget can be downloaded to Windows and copied into System32 and it works. Very convenient.
* "export" equivalent on windows is "set"
* flask run looks for the env variable FLASK_APP and will try to run it - if you set that env variable and flask run the app will run
* wget -O- outputs the output directly in the console as opposed to a file, saves time. O stands for output and the subsequent - indicates the console is the output.
* Edit: apparently curl has been part of Windows since 2017, so it now exists. It works, but annoyingly seems that all quote characters have to be escaped... This works: >curl -i -X POST 127.0.0.1:5000/names -H "Content-Type:application/json" -d "{\\"firstName\\": \\"Frodo\\",  \\"lastName\\" : \\"Baggins\\" }"
* If a class inherits object it's to maintain Python 2 compatibility - otherwise useless https://stackoverflow.com/questions/4015417/why-do-python-classes-inherit-object
* Difference between *args and **kwargs - args is for input without keywords (e.g. 1, 2, kwargs is for keyword input (e.g. {"Value 1":1, "Value 2: 2})

### Day 7: October 10, 2022

**Today's Progress**: Very short session due to travel. Added a basic method for drawing cards in Arboretum.

**Learnings:**
* For a button, use the < form > tag to specify the URL to navigate to and method (POST/GET) and then < input > to create the button. < button > never seems to be used.

**Project** https://github.com/mauritz2/arboretum

### Day 8: October 11, 2022

**Today's Progress**: Continued on the web app - the full game loop of a turn is in place, for two players (!))

**Learnings:**
* Currently using a lot of hard coded pixel values in the CSS. Better way: (1) pixels for pixel-related things (e.g. borders) (2) em/ex for text-related things (e.g. fonts),
  (3) %-based things for other elements such as columns. This makes the page more adapted to different window sizes and zoom levels. https://stackoverflow.com/questions/2915508/is-it-bad-to-work-with-pixels-in-css
* eval() can be used to turn a str representation of a tuple into a Tuple. E.g. turning "(1, 1)" into a (1,1) Tuple. Very cool!
* import Enum through "from enum import Enum"
* Reference the value of an enum by Class.VARIABLE.value
* To hover a class that's assigned to an input I had to nest it like input.myclass:hover to make it work
* Pillow can be used to programmatically edit images, e.g. adding text to .pngs
* I ran into an issue where editing an image would distort the colors. Converting to RGB as follows resolved it: my_image = Image.open(filepath).convert('RGB') https://stackoverflow.com/questions/61999451/pil-imagedraw-text-color-changes-to-blue
* Pathlib is very intuitive. Just create a base_path = pathlib.Path("../base"). Then easy to add a new path with slash, e.g. base_url / "hello.png"
* The difference between set and with in Jinja2 is that with creates a var scope that can be ended through {% endwidth %} https://stackoverflow.com/questions/53132094/whare-are-the-difference-between-set-and-with-in-jinja
* onmouseover and onmouseout can be used to change the src of an img on hover, apparently not possible through CSS
* Apparently best practice is to use img tags if the user will interact with the img, background-imgs for things that are just design
* To make a container 100% width in Bootstrap - set it to container-fluid

**Project** https://github.com/mauritz2/arboretum

### Day 9: October 12, 2022

**Today's Progress**: Continued on the web app, re-arranging UI elements and made them look nicer. Starting to look a lot better now.

**Learnings:**
* Ctrl + D copies the selected statements in PyCharm
* border-radius rounds corners on images - looks much nicer than having square images
* transition is cool - you can give a class new properties and add transition to "tween" between the property values
* scale() can be used to set the scale of an UI element, e.g. enlarge on hover

**Project** https://github.com/mauritz2/arboretum

### Day 10: October 13, 2022

**Today's Progress**: Continued on the web app, working through getting the scoring data to the UI and visualizing it. Need to be able to dynamically highlight cards based on what tree the user selects, which Jinja couldn't do so working through it in JS.

**Learnings:**
* JavaScript supports dot notation for referencing dict values. Can reference ```my_dict.my_key``` when dict looks like this: ```my_dict = {"my_key":"value"}``` 
* Syntax to loop through a dictionary in JavaScript:
```
  for (const [key, value]) of Object.entries(my_dict)){
    console.log(key, value);
    }
```
* Syntax to loop through an array in JavaScript to run a function on each item:
```
  my_array.forEach(function(array_item){
    console.log(array_item);
    }

```
* To append to an array in JS:
```
arr.push(element);
```

**Project** https://github.com/mauritz2/arboretum

### Day 11: October 14, 2022

**Today's Progress**: Finalized a first pass of the web app. Started some re-factoring.

**Learnings:**
* PyCharm commands:
* ```Ctrl + Tab``` cycles between recent files. Useful when having a split screen and going between screens.
* To split the screen: ```Ctrl + Shift + A``` opens up the action command. Then type Split to get the split options. Can be used to unsplit as well.
* To easily see the definition of a function: ```Ctrl + Shift + I``` when mousing over a variable or function. Then ```Enter``` navigates there, if needed.
* It's possible to nest row and column classes in Bootstrap. Pretty useful.
* Bootstrap won't use columns not defined. So defining one col-2 and one col-6 leaves 4 columns unused to the right.

**Project** https://github.com/mauritz2/arboretum

### Day 12: October 17, 2022

**Today's Progress**: Re-factoring the game logic, improving documentation and test coverage

**Learnings:**
* The most useful test cases are the tests for edge cases - e.g. index out of range issues. 
Having them fail when refactoring is a good reminder on edge cases to consider. 
I should write more edge case test cases. Also do a bit more TDD when writing a new func to think through the edge cases,
e.g. look for KeyErrors, IndexOutOfBound errors.
* The most common bugs I introduce are IndexOutOfBounds/KeyErrors, and >= errors. When writing > consider 
what should happen in the == case. When referencing a list: consider what will happen if list index is out of range. When
referencing a dict: consider if it's possible to reference the dict with a key that doesn't exist.
* itertools (import itertools) is useful to get permutations and cartesian products of lists
* Flask-SocketIO can be used to create a socket connection for Flask
```
var socket = io(); 
io.emit("my_event", {"data":"my_data"})
```
Can be caught on the server-side by Flask-IO:
```
@socketio.on("my_event"):
def handle_event(data):
  print(data["data"])
```

**Project** https://github.com/mauritz2/arboretum

### Day 13: October 18, 2022

**Today's Progress**: Starting to incorporate Flask-SocketIO to support multiplayer. Learning more JS and JQuery.



**Learnings:**
* It is possible to write test cases for Flask views https://flask.palletsprojects.com/en/2.0.x/testing/. Pretty cool, 
but seems redundant for a small project like this where the main thing that can go wrong is the game logic.
* ```;``` can have an impact on code running in JS. Trying this code will fail - removing the ```;``` makes it run
```
if (is_true){
  console.log("Hello")
  };
else if (is_true){
 ...
 } 
```
* Arrow functions in JS (defined through ``` => ```) are the equivalent of lambda functions in Python, e.g. anonymous functions
* Common pattern: Flask backend does ```json.dumps(my_dict)```, then JS frontend does ```JSON.parse(my_dict)```
* To get a value of an element using Jquery you can use ```$("#my_id").val()```. To set an ID, just give the new value as input to val. ```$("#my_id").val("new value")```!
* Use ```$("#my_element_id").empty();``` to clear out an element using JQuery
* Use ```$("#my_element_id").append(<HTML goes here>);``` to append to an element using JQuery
* If a JS function that triggers on form submit doesn't return anything the form will be submitted to the server (i.e. page refresh).
Adding ```return false;``` at the end of the function that runs on form submit fixes this so the page isn't refreshed https://stackoverflow.com/questions/13872761/html-javascript-page-is-resetting-after-submitting-form
* classList.add("class1", "class2") can be used to add two classes to a DOM element   
* var declares a global variable, let declares a variable within the specific scope its defined
* On the server side flask-io: by default emit() just sends a message back to the sender! To make it reach all SIDs, use the ```broadcast=True``` flag

**Project** https://github.com/mauritz2/arboretum



### Day 14: October 19, 2022

**Today's Progress**: Continued learning about Socket-IO and Flask-SocketIO. 

**Learnings:**
* I run into issues because it seems like the session ID (SID) keeps changing. It changes on form submit. Doing return false;
seemed to fix it, but it keeps coming back so there's something more fundamental I don't understand about sessions/sockets.
Reading the code on managing sessions and the documentation to understand it better. This was helpful to understand what a request is in flask: https://flask.palletsprojects.com/en/2.2.x/reqcontext/
and why I could only make request.sid work with the @socket.on decorator, i.e. only when there's an actual request.
* https://stackoverflow.com/questions/67463562/flask-socket-io-returns-different-sid-each-request
* https://stackoverflow.com/questions/14849188/constant-flask-session-ids this was also helpful for understanding SIDs
* https://stackoverflow.com/questions/15156132/flask-login-how-to-get-session-id
* Found this that warns to not use socket-io SIDs as IDs since they are ephemeral... https://socket.io/docs/v4/client-socket-instance/ 
* The best solution seems to have the unique identifier as a cookie on the client-side.  

**Project** https://github.com/mauritz2/arboretum

### Day 15: October 20, 2022

**Today's Progress**: Continued learning about Socket-IO and Flask-SocketIO. 

**Learnings:**
* Fixed the issue with the changing SID by making Flask put a cookie in the browser that I use to map to the player names.
That mapping is stored in sessions["uids"] and can be retrieved through sessions.get["uids"]. However, whenever I navigate to a new page
all the session variables disappear... It's not clear to me why. This was helpful in understanding Flask sessions https://overiq.com/flask-101/sessions-in-flask/
I might need to go to Flask-Sessions and move to server-side sessions or something. Because something odd seems to be happening at the
client side that keeps re-setting the session.
* This seems to indicate that there are two sessions: one for HTML and one for Flask-SocketIO https://blog.miguelgrinberg.com/post/flask-socketio-and-the-user-session
This post also seems to indicate that the best solution is server-side sessions. That's what I'll try next.
* Update: That fixed it! Setting cookies and server-side sessions is the way to go.
* JSON.parse() in JS is pretty useful. It can turn the str "true" into the boolean true. Better than eval(my_bool) which is a security risk
* When telling Jquery to listen for submit at class "test", "test" has to exist. So if I'm dynamically adding HTML
elements, then I need to add the listener after they exist. The listener is not applied at runtime.

**Project** https://github.com/mauritz2/arboretum

### Day 16: October 21, 2022

**Today's Progress**: Continued re-building the Arboretum web app using Socket-IO and Flask-SocketIO. 

**Learnings:**
* Going to re-build so that there's a single update board state event to be emitted. Sending too many emits back and forth is very bug prone and hard to troubleshoot.
This emit from the server-side will contain all the needed data to refresh the board (e.g. cards, current player etc.). It will be sent back
every time the client-side performs an action (e.g. emit(draw card) etc.)
* I'm very glad I built with normal app routes first before socketio. Almost all app routes have to be changed to socketio.on() routes
now. But now that I understand how socketio works, it will be much easier to build it from scratch with socketio() next time.
Also interested in learning React, I think that will be my next project. There must be an easier way to deal with all this client-side JS.
* Keep forgetting: HTML elements need to be created before they can be referenced. Jquery won't throw an error, the selector just won't find anything.
* Getting some unexpected behavior from my global var that keeps track of the mapping between the cookie IDs and player names.
I thought I could use global vars for development, but seems like everyone is saying Redis is much better so will implement that for global data and see if it works.
* Getting Redis to run on Windows is a bit tricky. Settled for a solution where I'm not even using server sessions anymore. Just a cookie and a global var.
It's stable now and managed to make each player take their turn. The app feels so much nicer now that it doesn't have to refresh the page on each action. The only thing that requires a refresh
now is the board. Will build it out on Monday to update through socket emits and JS.

**Project** https://github.com/mauritz2/arboretum


### Day 17: October 24, 2022

**Today's Progress**: Did a first complete version of the Arboretum app using Socket-IO - multiple players can now play 
through an entire game 

**Learnings:**
* To loop through keys in a JS dict you can use Object.keys(my_dict). E.g. 
```
for(const key of Object.keys(my_dict){
console.log(key))
}
```
* onsubmit="return false" on a < form > prevents page refresh on page submit
* A dict in JS can have integer keys, but they will be converted to strings
* ```Array.from()``` can be used to turn another datastructure into an array in JS
* HTTP status code 400 is the server complaining that the client sent it a request it doesn't understand
* There's a big difference between ```key IN Object.keys()``` and ```key OF Object.keys()```. keys of Object.keys() returns the expected keys, the other just an index starting from 0
* The code below results in logging undefined. Not passing a value for a parameter results in that param being "undefined" in JS. There's no error :-)
```
my_func()
function my_func(my_param)
{ console.log(my_param)}
```
* ! is a boolean flip in JS. 
```
my_bool = true;
console.log(!my_bool);
>> false
```

**Project** https://github.com/mauritz2/arboretum

### Day 18: October 25, 2022

**Today's Progress**: Re-factoring and updating the design to make it look better 

**Learnings:**
* Shortcut for multiple cursors in PyCharm: (1) select all rows, (2) shift + alt + g. Then use home and end to go to start and end of line.
* It's possible to fade in text using CSS @keyframes. Very useful for a game.
* Running into module error issues after re-factoring the folder structure. This was helpful: https://stackoverflow.com/questions/50745094/modulenotfounderror-when-running-script-from-terminal. This helped resolve the issue. 
* If your flask app file is called app.py you don't have to specify  ```flask --app {name} run```. You can just do ```flask run```.
* Aligning images and text in bootstrap requires ```d-flex justify-content-center text-center```

**Project** https://github.com/mauritz2/arboretum

### Day 19: October 26, 2022

**Today's Progress**: Very short session. Tried to fix a bug where zoomed images get put behind other images in a weird way.

**Learnings:**
* Seems like each < td > in a table gets its own z-index (or equivalent). So when I zoom (i.e. scale up one < td >)
it gets put ABOVE all the tds that were rendered before the scaling < td > and BELOW all the ones that were rendered after.
Have tried to remediate this by setting the z-index of cells etc. but haven't been able to fix it.
May need to re-build the zoom-functionality into something better. E.g. maybe a text pop-up of what the card is?
Definitely less elegant though. Would prefer if the image just got bigger.

**Project** https://github.com/mauritz2/arboretum


### Day 20: October 27, 2022

**Today's Progress**: Continued final touches on the web app

**Learnings:**
* Finally fixed the issue with overlapping < td >s. Setting the < td > to ```position:relative``` and the z-index of the < td > to 1, but 2 on :hover fixed it.
Setting the z-index on the zoom class I use to apply the zoom didn't work. It has to be on the td itself for some reason. I should look more into ```position:relative;```, ```position:absolute;``` etc.
to understand it better.
* Seems like static methods are an accident in Python and shouldn't really be used, interesting. (1) https://www.webucator.com/article/when-to-use-static-methods-in-python-never/, (2) https://testing.googleblog.com/2008/12/static-methods-are-death-to-testability.html

**Project** https://github.com/mauritz2/arboretum

### Day 21: October 28, 2022

**Today's Progress**: Continued final touches on the web app

**Learnings:**
* Looking into how to set jQuery event listener on dynamically created DOM elements. It works  if I set the event listener in the same function as the element is created, but otherwise it doesn't work.
Apparently the event listener has a "selector" parameter as described here. But can't make that work. Maybe because my selector is nested multiple steps down from the parent. https://stackoverflow.com/questions/203198/event-binding-on-dynamically-created-elements
* Update: I tried it again but I set the event listener to ```$(document).on("submit", ".my_class", function(){...``` and now it works! This will make the code cleaner since the event listeners can be broken out.
* You can do both ```Object.keys()``` and ```Object.values()``` on an Object (i.e. dict). ```Object.entries()``` is similar to enumerate in Python

**Project** https://github.com/mauritz2/arboretum


### Day 22: October 31, 2022

**Today's Progress**: Deployed Arboretum to AWS EC2. It's now officially done.

**Learnings:**
* Running a Flask app on host 0.0.0.0 makes it run on the public IP of the server.
* By default, an EC2 instance doesn't allow inbound traffic. I had to create a new inbound traffic security group for TCP.
* Not sure why, but locally I could find "my_folder/oak 1.png" using the path "my_folder/Oak 1.png". But when deployed to EC2 on Ubuntu, the paths
became case-sensitive. To keep in mind going forward: make all paths lower case.
* Using WinSCP was the easiest way to transfer data to the EC2 instance.
* Had to use PowerShell to run ssh-add to add the private key to connect to the EC2 instance. Doesn't seem like it's supported in the default console.
* ```app.debug = True``` doesn't work when with socketio. But running ```flask --debug run``` works.

**Project** https://github.com/mauritz2/arboretum

### Day 23: November 1, 2022

**Today's Progress**: Spent today learning more about CSS and React.

**Learnings:**
* My next project I won't use Bootstrap. I want to learn CSS at a more fundamental level.
* CSS has two layout systems: Flexbox and Grid.
* #### Flexbox
  * Flexbox: can result in horizontal scrolling. Unless you do ```flex-wrap: wrap;```
  * By default, a flexbox container is a row. And all children are columns.
  * The columns are independent of each other.
  * In flexbox you often have to reference the children (i.e. specific rows) and specify their behavior. In grid you mostly don't do this.
  * Good for navigation bars (by default each column is as big as it needs to be - i.e. intrinsic sizing)
* #### Grid
  * The default grid container adds rows. Can be changed through  ```grid-auto-flow: column;```. Then it behaves very
  similar to flexbox. 
  * ``` grid-template-columns: repeat(4, 1fr);``` creates four columns 
  * The grid sets things up in a 2D grid from the start, e.g. columns can stretch to match columns around it
  * Excels when you need a rigid system from the parent (i.e. no intrinsic sizing)
* Conclusion: Grid is a rigid structure you can plug content into. Flexbox is when the content determines box size.
* You can mix flexbox and grid together.
* Grid is easier to get started with (allegedly). More properties are needed. But it's more obvious.
* #### Absolute vs. Relative
  * Absolute = you can set the exact position and the rest of the elements will ignore this element when positioning.
  * Absolute will look for a parent that has a position = relative. If there is none, it will default to being relative to tbe body.
  * If you do top:0; bottom 0; it will by default be relative to the body, but if you have a parent with relative it's now relative to that parent.
  * If you have absolute you can use z-index on it.
  * If you need to add a z-index on an element that should stay in the line of the flow of the DOM you can apply ```position:relative;```. 
  * Without a value for the position property, the z-index doesn't work. This explains why the z-index didn't work with the cards in Arboretum.
* #### CSS Specificity
  * The last CSS specification wins. E.g. if you define the body text color multiple times the last one in the document is applied.
  * Specificity order: inline styles > IDs > classes > elements. Never use inline styles, it gets too messy.
  * Do not use !important.
* #### Media queries
  * Media queries(```@media() {}```) are rules for when CSS selectors should apply (e.g. based on screen width)
  * Make sure that Media queries come AFTER the selectors that you want to overwrite. The latest selector wins in CSS.
  * Media queries can apply on orientation (e.g. portrait and landscape) or how things should look on screen or print.
* #### React
  * Can't use ```class``` in React (JSX). Have to use ```className```.  
  * JSX elements can only have one element (i.e. everything needs to be wrapped in a <div> or similar).
  * Component.propTypes {} can be used as type hinting. The IDE will flag if the wrong type is used.
  * useState isn't mutable - its one-way data. When useState is defined, you define the state but also the func to call to change the state. E.g. as below:
  ```
    const [recipies, setRecipies] = useState({initial_state})
    ```
  * If you don't want to wrap a React component in a div or similar it supports having ```<>``` and ```</>```.
  * package.json holds all the dependencies. Running npm -i {package} automatically adds it to this file.


### Day 24: November 2, 2022

**Today's Progress**: Continued on the React tutorial

**Learnings:**
* To filter out data with ID 5
```
tasks.filter(task) => task.id !== 5
```
* If you're passing a function to a component, pass it as ```myFunc```, not ```myFunc()```
* The spread operator can be used to set a specific variable in an object:
```
recipies.map((recipie) => recipie.id === 1111 ? {... recipie, tasty: true} : recipie
```
* Remember to pass all Props as objects, e.g. ```({onCreate})``` as opposed to ```(onCreate)```
* If you don't care about the else in a ternary statement it's possible to use ```{my_bool && whatToDoIfTrue}```
* ```npm build``` creates the production build. It creates what to deploy in the build folder.
* json-server can be used to mock a backend when developing React apps.
* useEffect in React can be used to make things happen on page load.
* Add ```headers {}``` in plural to a POST request, not ```header {}```.
* The ```react-router-dom``` package is used in React for routing.
* To prevent page refresh when navigating to a new page, import Link from react-router-dom through ```import {Link} from "react-router-dom"```.
Then replace the ```<a>``` tag with ```<Link>``` and the ```href``` with ```to```. 
* In order to hide elements on certain pages, import useLocation through ```import {useLocation} from "react-router-dom"```.
In the component you can find the current route through ```const location = useLocation()``` and then check ```location.pathname === "/"```
to hide/show components.
* To get an f-string equivalent in JS: use a "backtick" (i.e. `) together with ${var} as below:
```
const fav_fruit = "Banana"
console.log(`My favorite fruit is ${fav_fruit}`)
```
* Changes to package.json don't apply until the server is re-started
* useState returns a getter and a setter
* When using React with a Flask backend - set a "proxy" in the package.json to the Flask API endpoint. Any fetch() request will be redirected to the Flask API.

### Day 25: November 4, 2022

**Today's Progress**: Decided to start building a running plan tracker for 80/20 training plans using React

**Learnings:**
* Ctrl + L to select a row in VS Code
* Somehow when running json-server, doing 127.0.0.1:3000/data doesn't work. But localhost:3000/data does work.
* To set a bottom border, do ```bottom-border: solid;``` To reduce the width of the border do ```border-width: 0.5px;```
* The basic React component syntax is 
```
import React from "react"

const MyComponent = () => {
  return (

  )
}
export default My Component
```
* To duplicate a line in VS Code: ```Shift + Alt + Down```
* To comment out a row: ```Shift + Alt + A```
* All the props I was passing to a component came out as undefined. Making the props into state using useState, setting the state, and then passing the state as prop solved the issue. Not exactly sure why. Maybe it's not possible to just pass a variable as a prop, you can only pass state?
* .map() is essentially a python for loop:
```
my_array = ["Banana", "Apple", "Pineapple"];
my_array.map(fruit => console.log(fruit));
```
* To set up a grid with 7 columns:
```
display:grid;
grid-template-columns: repeat(9, 1fr);
```
* Store anything that's not used at compile in the "public" folder, i.e. favicons. Any images used in compile, e.g. within components, should be in src
* It's not possible to use loops as part of the return statement in a React component. Do the for loop outside of the return, e.g. push to a list and then call it in the return through {my_list}: https://stackoverflow.com/questions/22876978/loop-inside-react-jsx
* It's possible to cause infinite rendering loops in React https://alexsidorenko.com/blog/react-infinite-loop/. Need to be smart about how to update state.
* ```fetch``` is always async https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch. Therefore it will always return a promise. I.e. as soon as fetch is called the next line of code will execute (in the absence of await). Get the value of promises using ```then()```.
* Components will start rendering before fetch completes. It's possible to return null if a Prop has .length 0. This prevents the component from failing. Better way is to await the fetch somehow.
* If you don't pass in [] as the second parameter to ```useEffect``` an infinite loop is created
* The default value in useState({value}) can matter a lot. E.g. browser will throw an error that map doesn't exist if the default value isn't []

### Day 26: November 5, 2022

**Today's Progress**: Continued building the running plan React app

**Learnings:**
* some() is the equivalent of any() in Python

### Day 27: November 7, 2022

**Today's Progress**: Continued building the running plan React app

**Learnings:**
* ```display: inline``` means elements that would normally line break won't, e.g. < p > elements. Width and height cannot be set for inline items.  ``` display: inline``` means the opposite. The element will take the full width. But you can set its width and height. ``` display: inline-block``` is an inline element for which width and height can be set.

### Day 28: November 8, 2022

**Today's Progress**: Continued building the running plan React app, mainly worked on layout and CSS. Finished draft of main workout plan view. Started on routing to other screens.

**Learnings:**
* If adding a class ```&&``` as a ternary doesn't work because it will add "false" as the class name. Better to use ```?``` and then ```: ""``` to make sure it doesn't add anything extra as a class.
* Both ```return()``` and ```render()``` can be used to create DOM elements within a component. ```render()``` is for writing React components wth class methods. I should use ```return()```.

### Day 29: November 9, 2022

**Today's Progress**: Continued building the running plan React app, building new component for plan selection.

**Learnings:**
* Side effect examples in React: fetching data, setting up a subscription, manually changing the DOM in React.
* ```useEffect``` is similar to ```ComponentDidMount```, ```componentDidUpdate```, and ```componentWillUnmount``` combined.
* There are two types of side effects in React: those that require cleanup and those that don't.
* Without cleanup = we can run them and forget. Example: logging, network requests, manual DOM mutations. The ```render()``` method should NOT cause side effects in React class components. Generally you want to run the side effects after you've updated the DOM. That's why side effects are put into ```componentDidMount``` and ```componentDidUpdate```.
* However, one drawback is that you often have to put the same side effect in ```componentDidMount``` and ```componentDidUpdate``` since you want to do the same thing on component create and update.
* ```useEffect``` means that you want React to do something after a component renders.... This explains all the issues I was running into when the DOM was relying on variables that existed within ```useEffect```. The DOM can't rely on stuff in ```useEffect``` for an initial render. 
* By default, React will REMEMBER what you put into useEffect and run it after the DOM is rendered. 
* Example of side effect that requires a cleanup: setting up a subscription to an external data source. In that case we need to clean up so we don't introduce a memory leak.
* ```./``` indicates same folder. So import ```./Button``` if the Button component is the same folder as the file that's importing it.
* State of children should be managed at the parent level.
* ```onClick={onViewClick()}``` will automatically call the function on render! To resolve do ```onClick={ () => onViewClick() }```
* To make certain rows in a grid different width: create a new class called wide or similar. Apply to to the cell. Then experiment with
```grid-column: 2/5;```
* So funny... the reason ```localhost:3000``` would work but ```127.0.0.1:3000``` would not is because my browser is resolving localhost to IPV6. Doing ```[::1]:3000``` works.
* ```PUT``` vs. ```POST```: ```PUT``` ensures idempotence, meaning that the same ```PUT``` call has the same effect. ```x = 5``` is idempotent. ```x ++``` is not idempotent. If idempotence is needed, use ```PUT```. Otherwise, ```POST```. 
* According to Google, dashses are preferred over underscores in URLs.
* Running into issues because ```PUT``` and ```DELETE``` requires an ID in json-server. If the ID isn't there they'll return 404 does not exist even if there's something there. Will have to re-define API so there's an ID for current-plan, even though there's just a single element there.

### Day 30: November 9, 2022

**Today's Progress**: Continued building the running plan React app, finishing plan selection first pass and doing first pass of heart rate zone setup.

**Learnings:**
* Use ```Math.round()``` to round a number in JS.
* Adding the ```readonly``` attribute within an ```<input>``` tag makes the text read-only, but it's still selectable.
* If somethinng is defined as a component state, the component will re-render on every state change.
* If a component will mount/unmount, consider where its state will live because it won't persist. Options: store the state in the component's parent or some type of local storage. 

### Day 31: November 13, 2022

**Today's Progress**: Created a script to generate secret santa matchings.

**Learnings:**
* Full script:
```
import pathlib 
import random
# Config
people = ["Person A", "Person B", "Person C"]

# Generate secret santa pairs and write to .txt
base_path = pathlib.Path(__file__).parent
to_receive_gifts = people.copy()
to_give_gifts = people.copy()

for person_to_give in to_give_gifts:
    person_to_receive = random.choice(to_receive_gifts)
    
    while person_to_receive == person_to_give:
        person_to_receive = random.choice(to_receive_gifts)
    
    to_receive_gifts.remove(person_to_receive)
    file_name = f"Till {person_to_give}.txt"
    with open(base_path / file_name, "w") as f:
        msg = f"Hej {person_to_give} : du är secret santa till {person_to_receive}"
        f.write(msg)
```
* ```then()``` doesn't resolve a promise into a value, it just returns a new promise.
* ```() => x``` is short for ```() => { return x; }```. That's why I sometimes get syntax errors when adding ```{}``` after ```then()```
* "If the previous handler started a promise but did not return it, there's no way to track its settlement anymore, and the promise is said to be "floating" [...] Therefore, as a rule of thumb, whenever your operation encounters a promise, return it and defer its handling to the next then handler.
* ```.json()``` is asyncronous because the ```fetch()``` call only reads the headers. To parse the body as JSON you need ```.json()```, which is defined asyncornously since you're still reading an incoming request. The parsing of the data isn't asynchronous, just the retrieving of the data.

### Day 32: November 15, 2022

**Today's Progress**: Continued on the React running app

**Learnings:**
* There's something I don't understand about return data after a fetch. It always returns a promise, even when it looks like the ```then()```s are chained correctly. The thing that always works is setting the state at the inner-most loop. 

### Day 33: November 24, 2022 - Half way!

**Today's Progress**: Back from some time travelling without a laptop. Watched some videos on CSS and continued on the running app. First pass at the app using json-server is close to done.

**Learnings:**
* CSS properties
  * ```line-height``` sets the height between lines. The default in most browsers seems to be around 1.1-1.4. Headers can look much better with a lower line-height. Parragraphs can look better with a larger line height.
  * ```gap``` can be used in a grid to easily create space between cells.
  * ```is()``` and ```where()``` applies CSS to all the items in a list of selector. Used to write more compect CSS.
  * The HTML attribute ```srcset``` is used to dynamically change images based on media queries.
* Updating a specific value at a URL is not easily done in REST. But one way to do it is through PATCH. The most common pattern is to do a GET, update the object, and then PUT it back. This was helpful: https://www.mnot.net/blog/2012/09/05/patch. Apparently JSON Merge Patch can also be used (?)
* I keep forgetting the ```[]``` after ```useEffect```. Forgetting this causes infinite loops in React.
* Flask-Migrate is a Flask adaptation of Alembic. Alembic is a database migration tool for SQLAlchemy.
* Seems like Flask runs better with venv than Conda. I get module not found errors with ```flask run```. Flask run doesn't seem to run within the conda env. Never resolved here https://stackoverflow.com/questions/59021000/flask-flask-run-not-working-in-conda-environment-windows-python-3-8-conda.

### Day 34: November 25, 2022

**Today's Progress**: Focusing on buliding out the Flask backend for the running app

**Learnings:**
* Refresher on OSI: Physical (bits), Data Link (frame), Network (packets), Transport (segment), Session (data), Presentation (data), Application (data)
* Four layers: Database layer, Persistence layer, Business layer, Presentation layer
* If your ```app.route("/url")``` is missing a trailing slash, Werkzeug will interpret that as that it should not match the URL if a user enters a trailing slash. You can also use ```strict_slahes=False```. Flask doesn't recommend disabling this though.
* Triple slash in a URI references localhost. E.g. ```"sqlite:///database.db"``` references localhost/database.db. Apparently Tim Berners-Lee regrets this triple slash: https://superuser.com/questions/352133/why-do-file-urls-start-with-3-slashes.

### Day 35: November 27, 2022

**Today's Progress**: Continued on building out the Flask backend for the running app

**Learnings:**
* Geting Flask application context errors when trying to populate the database with a script.
* To keep track of application-level data, Flask accesses current_app and g. This is to avoid having to pass the application around to each function. 
* ```current_app``` points to the application handling the current activity.
* Flask automatically pushes an application context when handling a request so that the view functions, error handlers, and other functions have access to ```current_app```. Flask also pushes an app context when running Flask CLI commands.
* Typically the app context has the same lifetime as a request.
* If you try to reference ```current_app``` outside of an application context, you get the error message that I'm getting. If you have direct access to the app, which I have, it's possible to manually push the app context. This command seems to fix the issue: ```app.app_context().push()```.
* The g object is used to store data in the application context. The g namespace object has the same lifetime as an application context. Data in g is lost after the context ends. So it can't be used to store data between requests. Sessions and databases are used to store data between requests. Example of what to store in g: database connection. 
* Flask-Marshmallow is used to JSON serialize the result of Flask-SQLAlchemy queries. Pretty convenient. 
* Define a Marshmallow Schema by 
```
class MyModelSchema(ma.Schemma):
class Meta:
  fields = ("id", "my", "fields")

my_models_schema = MyModelsSchema(many=True)
```
* Then use ```my_models_schema.dump(my_sqlalchemy_return_var)``` to JSON serialize.
* Developing using json-server first, creating the real Flask API later felt like a good idea. But migrating the data from json-server to Flask now feels like a lot of work... I wonder if there's a better way. Maybe setting up Flask routes but returning the data from there would be better? Then it's easy to change still, but at least the routes are set up. 
* I ran into an issue where Flask said I was overwriting URLs. In fact, it's the function names that need to be unique

```
app.route("/users")
def user():
  # return all users
```
```
app.route("/users/<user_id>")
def specific user(user_id): <---- This function needs a unique name, but it can use the same URL structure
  # return specific user
```

### Day 36: November 28, 2022

**Today's Progress**: Continued on building out the Flask backend for the running app

**Learnings:**
* The Flask module import error I ran into above was not due to ```flask run``` not detecting the Conda env. It's because the Flask cli module is weird. Running ```flask db init``` produces an import error as Flask can't import my modules. But ```python -m flask db init``` works without any issue.
* Marshmallow schema field naming errors fail without error. If the model has distance_km and the schema has ```fields = ("distance")``` the distance_km column will simply not be there in the returned JSON after ```dump()``` without any warning.
* If you want to serialize a single row from the DB, remove ```many=True``` in the Marshmallow schema. Otherwise it will complain that the returned data isn't iterable. I.e. if you only want to use ```MyModel.query.first()```, remove ```many=True```.
* ```my_date.isocalendar()[1]``` can be used to get the ISO week num of a week. This is the current week num, starting with Monday. ```my_date``` is a datetime object.
* To navigate to last cursor position in VSCode, use ```Alt + RightArrow``` and ```Alt + Leftarrow```.
* To navigate to actual last edit, use ```Ctrl + K``` and then ```Ctrl + Q```. This is very useful. But there's no history like in PyCharm...
* ```MyModel.query.delete()``` can be used to delete all rows in a table.
* To create a Flask conditional based on HTTP request type, do ```flask.request.method == "PUT"```.
* To get the JSON data from a request in a Flask view, do ```flask.request.get_json()```.
* This CSS is magic: ```mix-blend-mode: multiply;```. It makes white backgrounds in an image transparent. Works super well.
* There seems to be a significant difference between these ways of updating state. If I don't define a variable first, the state won't update properly. Maybe because we set the state to a promise in the second one... (?)
Good state update
```
...
.then((data) => {
let my_data = data["my_var"];
setMyState(my_data);
});
```
Bad state update - undefined
```
...
.then((data) => {
setMyState(data["my_var"]);
});
```
* This seems to be the best pattern to get the value from a fetch Promise.
```
const getMyData = async () => {
  const data = await fetch("/my-url");
  const dataJSON = await data.json();
  return dataJSON;
}
```
// Then in useEffect or some other function:
```
getMyData().then((result) => {
  // do something with the result
});

```
### Day 37: November 29, 2022

**Today's Progress**: Continued on the running app

**Learnings:**
* React state should be considered immutable! On state change, React only does a shallow check to check if the object is the same. If React thinks it's the same object it won't re-render the component (!!). Apparently if you use the spread operator ... React will consider it a new object.
* React has a Virtual DOM (VDOM), an abstraction layer on top of the DOM. Changes go to the VDOM first. Then Reacts diffs the VDOM vs. the DOM. React only updates the real DOM with what has changed.
* React schedules a render every time the state of a component changes. Scheduling means React will try to find the best time to re-render. When a component re-renders, all its child components re-render (!).
* As outlined above: if the reference to a prop stays the same the component won't re-render.
* State changes in React are asynchronous (!!). This explains why I get weird console log results as below:
```
console.log(myState):
>>> "my_val"
setMyState("my_updated_val");
console.log(myState);
>> "my_val" (?!)
```
* To create a CSS selector for a specific input type use ```input[type=text] {}```

**Project** https://github.com/mauritz2/eighty-twenty-running

### Day 38: November 30, 2022

**Today's Progress**: Continued on the running app.

**Learnings:**
* Modulus is the same in JS as Python: ```%```.
* ```.map()``` is an array-function. Can't be used for objects. But there are methods to turn objects into arrays. E.g. ```Object.entries(my_obj);```.
* If you use ```display:none;``` you can't have an animation of it going to ```display:block;```. Instead, always keep the element as ```display:block;``` but set height or opacity to 0. Then remove those constraints and animate that transition. Opacity 0 elements can still be interacted with though, so height 0 is probably best.
* Ran into an issue where a parent element had ```max-height:0px;```, but the child elements were still showing. Solution is to put ```overflow:hidden;``` on the parent element. 
* To do my transition I set ```max-height``` to 0, and then to 50000px when it should be shown. It didn't work because apparently that number is too high and not valid. Setting to 500px fixed it.

**Project** https://github.com/mauritz2/eighty-twenty-running


### Day 39: December 1, 2022

**Today's Progress**: Finished the running up. Next step is to try to deploy it.

**Learnings:**
* To set default value for props, import PropTypes.
* ```Ctrl + G``` and then a number navigates to that row number.
* ```Ctrl + P``` lets you navigate to a file by name. Very useful!

**Project** https://github.com/mauritz2/eighty-twenty-running

### Day 40: December 2, 2022

**Today's Progress**: Did the first two days of advent of code

**Learnings:**
* sort() doesn't return the list in Python, sorted() does return the list
* Forward proxy - lets a computer isolated on a private network connect to the public internet. Reverse proxy - lets a computer on the public internet connect to a private network.
* nginx can be used for multiple things, but relevant as a reverse proxy in Flask deployments. nginx is pronounced "engine x". It is the first to receive all the client requests. This is used for clients to be able to connect to the React app. Install in Linux through ```sudo apt-get install nginx```.
* To run the Flask API, Gunicorn can be used. Gunicorn is a web server Python package. Install through ```pip install gunicorn```.
* Run Guniorn through ```gunicorn -b 127.0.0.1:5000 api:app```. 

**Project** https://github.com/mauritz2/advent-of-code-2022

### Day 41: December 3, 2022

**Today's Progress**: Day 3 advent of code.

**Learnings:**
* ```string.ascii_lowercase``` can be used to get all lowercase letters.
* To get the intersection between multiple sets, do: ```set.intersection(set1, set2, set3)```. Sets can also be in a list: ```set.intersection(*set_list)```.
* ```str.strip()``` removes newlines from a string.

**Project** https://github.com/mauritz2/advent-of-code-2022

### Day 42: December 4, 2022

**Today's Progress**: Day 4 advent of code.

**Project** https://github.com/mauritz2/advent-of-code-2022


### Day 43: December 5, 2022

**Today's Progress**: Day 5 advent of code.

**Learnings:**
* Reading column data through ```open()``` isn't possible. But it's possible to do ```.readlines()```, then loop through each row and extract each column. 

**Project** https://github.com/mauritz2/advent-of-code-2022

### Day 44: December 6, 2022

**Today's Progress**: Day 6 advent of code.

**Learnings:**
* For Python regex import ```import re```.
* ```?!``` is negative lookahead. A char not followed by another char. E.g. to match an ```a``` not followed by a ```b```: ```a(?!b)```.
* ```?=``` is positive lookahead. I.e match an ```a``` followed by a ```b```: ```a(?=b)```
* ```re.match()``` only searches in the beginning of a string.
* ```re.search()``` searches anywhere in a string.
* Define a regex through ```r``` at the beginning of the regex str. Without the ```r``` I ran into an issue where the regex wouldn't match properly.

**Project** https://github.com/mauritz2/advent-of-code-2022

### Day 45: December 7, 2022

**Today's Progress**: Day 7 advent of code.

**Learnings:**
* A nested dictionary structure of arbitrary length is usually not the best way to go.
* Sum a dict: ```sum(my_dict.values())```.
* List comprehension for dict works. Return a dict with all values under 100:
```{k:v for k, v in my_dict.items() if v < 100}```.
* To add thousand separators to a f-string, simply add ```:,``` after your variable like ```f"Value: {my_var:,}```

**Project** https://github.com/mauritz2/advent-of-code-2022

### Day 46: December 8, 2022

**Today's Progress**: Day 8 advent of code.

**Learnings:**
* Lambda to strip each row of newlines
``` new_data = list(map(lambda x: x.strip(), old_data)) ```. Map doesn't return a list, therefore ```list()``` is needed.
* Deployed the running app to my Linux server used nginx and Gunicorn:
  * The app was loading but was 502 errors on API requests. Making project executable fixed it: ```chmod 0755 /to/project``` 
  * Removing the "proxy" in ```package.json``` seems to be a must
  * ```npm run build``` updates the build folder
  * Seems best to use routes that start wth /api or similar to make it easy for nginx to detect what's a local file and what's an API request.
* I should finally get the debugger running in VSCode. Today's advent of code took a lot longer because I didn't have it.

**Project** https://github.com/mauritz2/advent-of-code-2022

### Day 47: December 12, 2022

**Today's Progress**: Continued on my own game

**Learnings:**
* Got a lot of CORS errors on this app, which I didn't get on the running React app. To avoid: set up the ```proxy``` in the package.json. And DON'T use absolute URLs in ```fetch``` requests. That resolved the CORS issues this time.
* To select an interpreter in VS Code Ctrl+ Shift + P. Then "Python: Select Interpreter". It scans Conda and VENV envs automatically so select from drop-down.
* For ```socketio.on()``` - add an empty return at the end. Otherwise React waits for a long time for something to be sent back.
* Edit: Actually the return isn't needed. The issue was with how I initialized the SocketIOs socket incorrectly. Way that worked:
```
  const socket = io("localhost:5000/", {
    transports: ["websocket"],
  });
```

**Project** https://github.com/mauritz2/location-game

### Day 48: December 13, 2022

**Today's Progress**: Continued on my own game

**Learnings:**
* To pass an onsubmit event using TypeScript, the correct type is ```React.FormEvent<HTMLFormElement>```
* Use ```Ctrl+1``` and ```Ctrl+2``` to navigate between two split screens in VSCode


**Project** https://github.com/mauritz2/location-game

### Day 49: December 15, 2022

**Today's Progress**: Continued on my own game

**Learnings:**
* I should do more TDD again

**Project** https://github.com/mauritz2/location-game

### Day 50: December 16, 2022

**Today's Progress**: Continued on my own game

**Project** https://github.com/mauritz2/location-game

### Day 51: December 17, 2022

**Today's Progress**: Continued on my own game

**Learnings:**
* Conda randomly stopped working in the console. Had to re-install it again. Saving the env folder and then putting it back after re-install didn't save the envs.

**Project** https://github.com/mauritz2/location-game

### Day 52: December 18, 2022

**Today's Progress**: Continued on my own game

**Learnings:**
* React context = makes state universally accessible
* React code can go outside of the component code, e.g. when instantiating sockets etc.
* ```debugger``` causes the browser to break at that line of code

**Project** https://github.com/mauritz2/location-game

### Day 53: December 20, 2022

**Today's Progress**: Continued on my own game

**Project** https://github.com/mauritz2/location-game

### Day 54: December 21, 2022

**Today's Progress**: Continued on my own game

**Learnings:**
* ```!.``` in typescript indicates that the var can't be null. This prevents typescript from complaining that the var might be null.

**Project** https://github.com/mauritz2/location-game

### Day 55: December 23, 2022

**Today's Progress**: Continued on my own game

**Project** https://github.com/mauritz2/location-game

### Day 56: December 24, 2022

**Today's Progress**: Continued on my own game - fixing the state context for characters...

**Project** https://github.com/mauritz2/location-game

### Day 57: December 30, 2022

**Today's Progress**: Continued on my own game

**Project** https://github.com/mauritz2/location-game

### Day 58: December 31, 2022

**Today's Progress**: Started on Day 9 in Advent of Code

**Project** https://github.com/mauritz2/advent-of-code-2022

### Day 59: January 1, 2023

**Today's Progress**: Continued on Day 9 of Advent of Code. Set up the VS Code debugger finally. 

**Learnings**
* Ran into an issue when creating a 2D matrix that changing a value in one row changed the same value in all rows. Explained here: https://www.geeksforgeeks.org/python-using-2d-arrays-lists-the-right-way/. Best to avoid list comprehension or * when creating a 2D matrix in pure Python.  

**Project** https://github.com/mauritz2/advent-of-code-2022

