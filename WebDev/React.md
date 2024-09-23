![alt text](image.png)

![alt text](image-1.png)

![alt text](image-2.png)

Project files:
    1) Node_modules
        a. Holds all installed lib from npm.
    2) Public
        a. Favicon.ico
            i. React logo
        b. Index.html
            i. The html and dom for react application.
        c. Manifest.json
            i. Provides information about the project .
                1) Name
                2) Author
                3) Icon,etc..
        d. Robots.txt
            i. Used to prevent search engine and bots to crawl on the react application
    3) Src
        a. App.css
            i. Global css for react app
        b. App.js
            i. Global js component for react app
        c. App.test.js
            i. Global test directory for react app
        d. Index.css
            i. Css for index.html
        e. Index.js
            i. Main root component .Hooks onto the index.html file to be  able to start rendering components.
        f. .gitignore
            i. File to ignore in git
        g. Package.json
            i. Used for dependencies, defining project properties, description,author,licensing and more
        h. Package-lock.json
            i. Locks dependencies on specific version number and records versioning for installation.
        

    1) Creating the react project 
        a. npx create-react-app app-name
    2) Running react application.
        a. cd app-name
        b. npm start
            i. Builds the app
            ii. Starts the server
            iii. Watches the source files.
            iv. Rebuilds the app when source is updated
    3) Changing the port
        a. By default:3000
        b. set PORT=<port-num> && npm start
    4) Install latest package
        a. npm i tar
    
    npm start
        Starts the development server.
    
      npm run build
        Bundles the app into static files for production.
    
      npm test
        Starts the test runner.
    
      npm run eject
        Removes this tool and copies build dependencies, configuration files
        and scripts into the app directory. If you do this, you can’t go back!
    

npm install -g --verbose react-devtools



    1) Get links for remote bootstrap files.
        a. <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-9ndCyUaIbzAi2FUVXJi0CjmCapSmO7SnpJef0486qhLnuZ2cdeRhO02iuK6FUUVM" crossorigin="anonymous">
    2) Add links to index.html 
    3) Apply bootstrap css styles in component in html template
    4) Apply bootstrap css styles in component in html table

Component.js
--------------------
Pass values in functions:
function Component(props)
{
 const var=props.var;
<p> {var}</p>

}

Export default Component;


App.js
------------------------------------------
Import Component from "./Component.j"

<Component var={list[0].var}/>

Iterate List/Array:

  const list_item=[{
    rowId:"63826",rowName:"ABCD ",rowPlace:"Vellore"
  }]


{props.list.map(index =>(
 <component_name var1={index.var1} />
))}

When ever we use list we have to pass key value in list


Topics:
    1) Component
        a. Components are independent and reusable bits of code. They serve the same purpose as JavaScript functions, but work in isolation and return HTML.
    2) List
        a. constcars =['Ford','BMW','Audi'];
    3) Props
        a. React Props are like function arguments in JavaScript and attributes in HTML.
    4) Map
        a. {cars.map((car)=><Car brand={car}/>)}
    5) On-click [ Event Handlers ]
        a. <button onClick={shoot}>Take the Shot!</button> -> React
        b. <button onclick="shoot()">Take the Shot!</button> -> Html
        c. Pass argument in the on-click , here Goal is passed as argument.
            i. <button onClick={() => shoot("Goal!")}>Take the shot!</button>
            ii. const shoot = (a) => {
                alert(a);
              }
        d. Pass event type :
            i. <button onClick={(event) => shoot("Goal!", event)}>Take the shot!</button>
            ii. const shoot = (a, b) => {
                alert(b.type);
                /*
                'b' represents the React event that triggered the function,
                in this case the 'click' event
                */
              }
        e. If we use like this :
            i. <button onClick={shoot()}>Take the shot!</button>
            ii. It will rendered and go off so when ever we click its doesn’t work
    6) Hook -> UseState
        a. The React useState Hook allows us to track state in a function component.
        b. useState accepts an initial state and returns two values:
            i. The current state.
            ii. A function that updates the state.
        c. Example:
            const [car, setCar] = useState({
                brand: "Ford",
                model: "Mustang",
                year: "1964",
                color: "red"
              });
            
              const updateColor = () => {
                setCar(previousState => {
                  return { ...previousState, color: "blue" }
                });
              }
            
            
    7) Hook -> UseEffect
        a. The React useEffect Hook allows us to do some function whenever changes in the state field.
        b. Even without argument is also possible
        c. But if we didn't pass that then it will rendered so many times[infinite]. So it will affect react performance.
        d. Example:
            useEffect(() => {
                console.log("Screen Rendered");
              }
            , [car] // if we provide empty array then it renders initial
            );
            
        e. Let say whenever component renders initial do some action:
            i. Example:
                useEffect(() => {
                //some action
                  setCar(previousState => {
                      return { ...previousState, color: "blue" }
                    });
                    console.log("Screen Rendered");
                  }, [car]);
                
                
            
            

    • <Router>
        ○ A router allows your application to navigate between different components, changing the browser URL, modifying the browser history, and keeping the UI state in sync.
        ○ The React Router API is based on three components:
            § <Router>: The router that keeps the UI in sync with the URL
            § <Link>: Renders a navigation link
            § <Route>: Renders a UI component depending on the URL
        
    • DOM
        ○ DOM stands for 'Document Object Model'. In simple terms, it is a structured representation of the HTML elements that are present in a webpage or web app. DOM represents the entire UI of your application.
        ○ The DOM (Document Object Model) represents the web page as a tree structure. Any piece of HTML that we write is added as a node, to this tree. With JavaScript, we can access any of these nodes (HTML elements) and update their styles, attributes, and so on


To Set basename in router:
"start": "PUBLIC_URL=/tds react-scripts start"
"homepage":"./path"


Define variables:
Let <variable_name> : <type> = <initialize the variable>

Let flag:boolean=false;

Type Script is Strongly Typed:
    1) If one variable is defined as boolean , we should not assigne value with string.
    2) So in that case we have to use "any" type.

Template Strings:
    1) Console.log("Hi " +var1+ " "+ var2);
    2) Console.log(`"Hi " ${var1} ${var2}`);

If any compilation error occurs, but still js script will generate to stop that us the below command
    1) tsc - noEmitOnError sample.ts


Loop:
For (let i=0;i<=5;i++){
 console.log(i);
}

Declare an array:
Let array : number[] = [1,2,3,4,5]

For (let tempNumber of array){
     console.log( tempNumber );
}


Add element to array:
Array.push(10)
