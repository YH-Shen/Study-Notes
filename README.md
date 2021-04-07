# Study-Notes

# UI Component Library Project Notes

---

1.  [Project Highlights](#project-highlights)
2.  [Webpack Setup](#webpack-setup)
    -   [Setup Steps](#setup-steps)
    -   [Key Takeaways](#key-takeaways)
    -   [html-webpack-plugin](#html-webpack-plugin)
    -   [npm install & yarn install](#npm-install-&-yarn-install)
    -   [yarn.lock file](#yarn.lock-file)

---

## Project Highlights

-   webpack: used awesome-typescript-loader and html-webpack-plugin
-   circle ci
-   test coverage
-   auto test, auto bundle, and auto npm publish after push!
-   react router
-   used scss attribute selector to avoid interference
-   used react protal to prevent context stacking
-   have highlited code demo

Dialog:
onClose={() => {
ReactDOM.render(
React.cloneElement(component, { visible: false }),
div
);
ReactDOM.unmountComponentAtNode(div);
div.remove();
}}
re-render the component to change the attribute: visible. Cloned the component and then overwrite the property.
there was an extra div to remove: remove the events attached onto the div first with "ReactDOM.unmountComponentAtNode()". And then remove the div.

form validation
Asychornous validation with promise.all**\*** very complicated - challenge
Promise.all only accepts arrays. So I used nested arrays first. And then combine the nested arrays together into one long nested array. And then zip the array

## Webpack Setup

Used yarn (try to avoid npm), webpack 4, webpack-dev-server 3, TypeScript 3

### Setup Steps:

1.  Make directories and create library - used git repo
2.  npm init -y - creates package.json
3.  Create lib/index.tsx after installed webpack - yarn add webpack webpack webpack-cli -dev
4.  Create webpack.config.js: - setup entry, output, modeule.rules(jsx, tsx, scss), plugins - translates entry scripts with rules defined, and different loaders. - output to the absolute address defined. Use path.resolve to parse addresses for different operating systems. - ouput libraryTarget: use umd to accomodate for both commonJS and amd. - pack index.tsx into index.js
5.  Setup webpack-dev-server, and webpack.config.dev.js - webpack-dev-server monitors the 8080 port - webpack-dev-server also provides realtime translation of the tsx document into js strings in memories for faster speed - when the user visits the 8080/js document, the server takes the js strings in memory and presents it to the user - now we can use "npx webpack-dev-server" command to launch a server for development. or "yarn start" as defined in package.json
6.  Create index.html
7.  Setup webpack.config.prod.js
8.  Create examples preview and webpack config.doc.js
9.  Introduce tests
10. Introduce CI (continuous integration, used circle CI)
11. Setup tsconfig.json and tslint.json
12. Setup scripts (yarn start, yarn build, yarn test)
13. Customized tasks (yarn task create component x)

### Key Takeaways

1.  What do dev, prod, and test envrironments do?
2.  Why seperating these environments?
3.  Why do we generate index.html instead of mannually write one?
    -   The index.html scripts depends on the config setups in other scripts. Genertating the index.html automates the work flow and avoids possible human mistakes.
4.  What does CI do?
5.  How to start developing?

### awesome-typescript-loader

### html-webpack-plugin

A webpack plugin to automatically generate and update html file that includes all the webpack bundle and config updates.

### npm install & yarn install

#### --save-dev/--dev/-S-D

        ```linux
        --save-dev
        --dev
        -S-D
        ```

For pachages that are only used by developers.
Example: Webpack, TypeScript

#### --save/"nothing"/-S

        ```linux
        --save

        -S
        ```

For packages that are also used by users (users' browser).
Example: React, jQuery

--save is the default setting if nothing is added for installation.

### yarn.lock file (what is this file?)

1. The lock file for yarn. (gnerated when using yarn to manage npm dependencies.)
2. It locks down the versions for all the dependencies specified in the package.json file. Ther versions do not have to be the same as long as it works.

### Exclude React and react DOM from the packed bundle

Exclude React and react DOM from the packed bundle becasue the users of this react UI library definetrly have react installed already. Excluding by setting "externals" module in the webpack.config file:

```json
externals: {
        react: {
            commonjs: "react",
            commonjs2: "react",
            amd: "react",
            root: "React",
        },
        "react-dom": {
            commonjs: "react-dom",
            commonjs2: "react-dom",
            amd: "react-dom",
            root: "ReactDOM",
        }
```

### importing

Importing ADDRESS:
Use relative address if importing from your own file
Use library name if importing from third-party library.

importing default export:
import GIVEN_NAME from ADDRESS

importing named values:
import {PARA_NAME} from ADDRESS

importing a combination:
import GIVEN_NAME, {PARA_NAME, ...} from ADDRESS

### React Class this

#### Method 1:

define a function with format: x = () => {}

constructor(props){
super(props);
this.state = {
n: 1
};
}
...
x = () => {
this.setState({
n: 2
})
}

It is a simplified way of definining this.x in the consturctor. Therefore, this method has a problem of taking too much memory. Every case ran requies it's own definition of this.x.

#### Method 2:

Mannually bind this in jsx

<button onClick={this.x.bind(this)}>button</button>

#### Method 3:

Mannually bind this in the consturctor.

constructor(props){
super(props);
this.state = {
n: 1
};
this.y = this.x.bind(this)
}
...
<button onClick={this.x.bind(this)}>button</button>

Method 1 is the simplified version of method 3.

### Axios trick with useEffect hook

The empty second variable of useEffect hook makes it runs only once when mounted.
Perfect chance to use axios.get information here.

useEffect(() => {
axios.get('')
}, [])

### static importing and dynamic importing

static: suitable for tree-shaking optimization but not as convinent for importing many items
dynamic: scalable

### style loader, css loader, sass loader

sass loader translates scss doc into css doc as strings.
css laoder converts the css doc into an object with strings inside.
style loader converts the object into a style tag enclosing the css. general process as follows:

style_tag = document.createElement("style tag")
style_tag.innerHTML = "css"
document.head.appendChild(style_tag)

### npm version

major.minor.patch

commands:
(comes with auto git commit)
npm version major >>>> 0.0.1 -> 1.0.0 for major change in API, affects cuurent code
npm version minor >>>> 0.0.1 -> 0.1.0 for minor change in API, doesn't affect current code
npm version patch >>>> 0.0.1 -> 0.0.2 for bug fixes, no API changes

### React.ReactNode vs React.ReactElement

ReactElement can only take tags. ReactNode can take both tags and strings.

type ReactNode = ReactChild | ReactFragment | ReactPortal | boolean | null | undefined;

### Key Takeaways for Dialog Component

1. Use example for easier development
2. Used Scoped CLass (higher-order function) for quicker tag naming. Used "syhui-" prefix to avoid interference.
3. Used React Fragment to attach multiple divs without creating extra layer
4. Render element based on visbility: const output = props.visible && (<Fragment></Fragment>). or use props.visible? (render): null. If else is too much trouble.
5. Used React Portal to move the node away from it's original parent. Move the content to document.body to avoid context stacking or event bubbling.
6. Dynamically render/generate components: declare component as const. Attach the component inside a div, and then append the div onto document.body.
7. Pass API from enclosure: return a function that controls the varibale inside the enclosure

### Key Takeaways for Layout Component

1. Receive attributes for layout may overwirte pre-written classes.
   Deconstruct props first:
   const { className, ...rest } = props;
   And then join the pre-written class name with given classname to be the final className. Use "...rest" for the rest of the props attributes.
       <div className={[sc(), className].join(" ")} {...rest}>

    But this method is so inconnvienet... Then I improved scopeMaker function to takein the extra classname

2. Used Functional Programming to refactor scopedClassMaker!!!
3. Used NavLink for the "active" state displayment

### Component Options

1. General and widely applicable(ie. AntD), but is more complicated in use
2. Focused and customed(libraries used inside companies): less overall support but more user friendly and customized

### Controlled and uncontrolled component

Reccomend forms to use controlled components: useState as only source of truth.
Principle of React UI component: UI = f(state)

How to get the value of the controlled and uncontrolled input field?

controlled:
const [name, setName] = useState("syh")
<input value={name} onChange={(e) => setName(e.target.value)}/ >

uncontrolled:

const refInput = useRef<HTMLInputElement>(null);
const x = () => {
conosle.log( refInput.current!.value);
}
<input defaultValue={name} ref={refInput} type="text" onBlur={x}/>

### form difference from AntD

feedback all the value on change:

1. No need to reprocess the data.
2. Might be slow if there are tons of input, but it's a rare case
