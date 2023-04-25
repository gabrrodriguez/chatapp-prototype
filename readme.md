# Deloitte ChatGPT Prototype

## Demo Start Process
1. Fork the Git Repo [here](https://github.com/rodriggj/chatgpt-app)
> **NOTE:** You will have to be added to the Git Repo Collaborator list in order to access the Git Repository. To do this contact Gabriel Rodriguez via email at the following address: gabrrodriguez@deloitte.com

2. Clone the repository. 

3. You will have to open 2 terminal windows:
  + One for the `client` application
  + Another for the `server` application

4. In the `client` terminal window run the following commands
```s
cd client
npm run dev
```

5. in the `server` terminal window run the following commands
```s
cd server
npm run dev
```

6. Open a Browser window and navigate to the URL _http://localhost:5173/chat_

7. You will have to create users in ChatEngine {{ write process for this }}

8. In order to have the ChatGPT engine reply back you have to execute the following {{ write process for this }}

-----------

## Build Process
- [ ] [Initial Config](https://github.com/rodriggj/chatgpt-app#initial-config)
- [ ] [Chat Engine Config](https://github.com/rodriggj/chatgpt-app#chat-engine-config)
- [ ] [Initial Routing, Chat Component Create, Dir mappings, & Linting Config](https://github.com/rodriggj/chatgpt-app#initial-routing-chat-component-create-dir-mappings--linting-config)
- [ ] [Chat Component - Front-End Initial Config](https://github.com/rodriggj/chatgpt-app#chat-component---front-end-initial-config)
- [ ] [Header Component - Front-End Initial Config](https://github.com/rodriggj/chatgpt-app#header-component---front-end-initial-config)
- [ ] [StandardMessageForm Component](https://github.com/rodriggj/chatgpt-app#standardmessageform-component)
- [ ] [Initial Back End Configuration](https://github.com/rodriggj/chatgpt-app#initial-back-end-configuration)
- [ ] [Configure Inital Back End Routes](https://github.com/rodriggj/chatgpt-app#configure-inital-back-end-routes)

{{ Add remaining sections of Build Process }}

-------

## Initial Config 

1. In a terminal session enter 

```s
npm create vite@latest
```

A wizard will prompt you in your termial. Make the following config changes
- [ ] Ok to proceed: _y_
- [ ] Project name: _client_
- [ ] Select a framework: _React_
- [ ] Select a variant: _JavaScript_

2. When the scaffolding of the project completes enter the following: 
```s 
cd client
npm i
```

3. Add the following extensions in your IDE to enable your project. You can select these by the far left navbar in Visual Studio Code. (the blocks icon) and using the search functionality within VSCode to find these extensions.
<p align="center">
<img width="73" alt="image" src="https://user-images.githubusercontent.com/8760590/232827818-272095e7-d072-44c4-b7fd-f810d1a017f7.png">
</p>

- [ ] `ES7+React/Redux/React-Native snippets`
- [ ] `Prettier ESLint`
- [ ] `ESLint`

4. Back to the project, within the `client` directory we will install the following packages from the terminal by entering the following commands: 
```s
npm i react-redux @reduxjs/toolkit @heroicons/react react-router-dom react-dropzone react-chat-engine-advanced --save
npm i -D sass
```

> NOTE: The `sass` will be installed and listed in our package.json as a dev dependency. 

> Verify that the npm build process created a file directory that looks like the following: 
<p align="center">
<img width="233" alt="image" src="https://user-images.githubusercontent.com/8760590/232828263-5960b041-c71f-4807-bd1d-0091762be046.png">
</p>

5. In our `client/src/` directory we can make a few changes to the boilerplate files provided:

5a. Delete the file called `client/src/App.css` 

5b. Open the  `client/src/App.jsx` file remove the content and replace with the following: 
```js
function App() {

  return (
    <div className="app">app</div>
  )
}

export default App
```

5c. Open the file called `client/src/index.css`, and remove all the content and save the file. Rename the file to `client/src/index.scss`

5d. In the new file called `client/src/index.scss` add the content from the css library provided [here](https://github.com/ed-roh/chat-app/blob/master/client/src/index.scss).

5e. Open the file called `client/src/main.jsx` and update the import statement to point to the new `.scss` file, like so: 

```js
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import './index.scss'   //updated from './index.css' to './index.scss'
// ...
```

5f. Now lets verify that none of the changes broke the underlying code structure. Be sure you are in your `/client` directory, and from the terminal run the following command: 
```s
npm run dev
```

You should see no errors, but `vite` will create a URL and port where you can copy/paste into a browser session and you should see the application and the `app` text we modified above in Step 5b.  

Terminal Session Display
<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/232834757-0bf16503-12de-4a30-8b63-bbb74072f59e.png">
</p>

Browser Session Display
<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/232835158-80f774a1-e7c4-48a8-9281-d16021ea8331.png">
</p>

##### [Back To The Top](https://github.com/rodriggj/chatgpt-app#build-process)

--------

## Chat Engine Config

1. Go to [Chat Engine](https://www.chatengine.io) to sign-up for an account

2. When you create a new project give it a _Project Title_ enter `chat app`, and for _Promo Code_ enter `edward`, click _Create Project_. 

3. When the screen redirects you will be presented with a screen that looks like this, with API credentials. 
<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/233066482-83db1846-9744-461e-9cf0-615fbb59e6d0.png">
</p>

4. The next step is to create a user. On the left nav-pane is an option for _Users_, click this. A right nav-pane will appear, click _New User_. A form will appear and you will have to complete the form data. In the form data you will be asked to provide a secret, that can be anything (e.g 1234) -- it doesn't have to be the API secret from Step 3. The avatar is optional. When finished completing the form click _Create User_. 
<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/233068504-4c096bc8-ff1e-426d-b13f-48ad17296cbf.png">
</p>

5. When redirected back to the _Settings_ page for your project, we can now create a `Chat`. In the left navpage click _Chats_. When the right navpane appears click _New Chat_. Provide a _Chat Title_ `testchat1`. You can avoid the _Admin User_ and _Access Key_ for now. 
<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/233070530-7e8e49b8-cc6a-4f49-8e3c-4941fe24436e.png">
</p>

6. Before proceeding further, understand where to go for futher insight into the `Chat Engine` documentation. The link to the documentation can be found [here](https://chatengine.io/docs/react/v1). Realize there are 2 sets of documenation. The second set provides a bit more customization, more robust , and advanced features. 
<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/233071269-ef885e18-6fd9-4bf2-aca2-1b87ce5e1603.png">
</p>

Additionally if you want to utilize the `Chat Eninge` REST API, without interacting with the front-end UI, the documentation for this API can be found [here](https://rest.chatengine.io/).

Finally, if you need a breakdown of the Components used on the `Chat Engine` you can go here to the [Storybook](https://chatengine-io.github.io/react-chat-engine-advanced/?path=/docs/multichatwindow--default-story) and see a list of components and the assoicated props of each component. Or finally go [here](https://chatengine.io/docs/react/v2/components/list) which is where you can change the styling or customize the UI of the chat-engine. 

##### [Back To The Top](https://github.com/rodriggj/chatgpt-app#build-process)
---------

## Initial Routing, Chat Component Create, Dir mappings, & Linting Config

1. Start in the `client/src/App.jsx` file and enter the following imports at the top of the file: 

```js
import { useState } from "react"
import {BrowserRouter, Routes, Route, Navigate } from 'react-router-dom'
//...
```

2. Now, in the same file, set up our initial route to the `Chat` component that will be created later. 

```js
function App() {

  return (
    <div className="app">
      <BrowserRouter>
        <Routes>
          <Route path="/chat" element={<Chat/>}></Route>
        </Routes>
      </BrowserRouter>
    </div>
  )
}
```

3. Create out environment variables. Start within your root directory `/client` and create a file called `.env.local`. Then enter the following content for now in that file. 

```
VITE_BASE_URL=http://localhost:1337
VITE_PROJECT_ID=5fcd88fd-e426-40a5-aad6-d6b1e65e618f
```
> **NOTE:** We need to name our file `.env.local` because when using `vite` a `.gitignore` file is created that has a line `*.local` which is SCM to ignore any files that have a `.local` suffix. 

> **NOTE:** The `VITE_PROJECT_ID` comes from the _Chat Engine Project Id_. 

> **OPTIONAL:** At this point you may want to install some additional linting capability on the autosense in the IDE. Recommend you go to a terminal and install the following if you want additional autosense population/linting. 

```s
npm i -D eslint eslint-config-react-app
```

Additionally you will want to create an file to manage your linting config. To do this in your `/client` dir, add a file called `.eslintrc.json` and add the following code: 
```json
{
  "extends": "react-app"
}
```

With this config in place if you refer back to your `client/src/App.jsx` file, you can see that the linting has identified code in your react-app that needs to be addressed. For example the `Chat` component that was referenced but doesn't exist has a squiggly line indicating that it needs remediated. 

4. Now add some organization to the components that we will be creating. In `client/src/` directory create a dir called `components` and create a sub-dir to called `chat`. Finally create a file in the `client/src/components/chat` dir called `index.jsx`
```s
cd /client/src
mkdir components
mkdir components/chat
code components/chat/index.jsx
```

5. Inside the file `index.jsx` input the following code: 
```js
import React from 'react'

const Chat = () => {
  return (
    <div>
      <p>Hello from the Chat component!</p>
    </div>
  )
}
export default Chat
```

> **NOTE:** Using the autosense function, in the `index.jsx` file you can enter `rafce` which is a shortcut to creating an arrow function with an export, and the boilerplate code for this component will be created. 

6. To test that the component is working import the `Chat` component into the `client/src/App.jsx` file and you should see the text visible in a browser. Nav to `client/src/App.jsx` and update the import statements to now include the Chat component. 
```js
import { useState } from "react"
import {BrowserRouter, Routes, Route, Navigate } from 'react-router-dom'
import Chat from './components/chat'
//...
```

> **Optional:** You can see in the above import that we are making a mapping to the chat `index.jsx` file via a relative path mapping. As components get nested in a dir structure this can become very hard to keep track using the `../` or `./` notation. To avoid this we can set a mapping to the `src` folder. To do this we first need to install a Dev Dependency 
```s
npm i -D @types/node
```
> Then we need to update our `vite.config.js` file to provide an alias to src and the appropriate mapping. You can do so by updating the `vite.config.js` file with the following code: 
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from "path"

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: [{find: "@", replacement: path.resolve(__dirname, "src")}]
  }
})
```
> Next, we need to add one more config file, to the `/client` dir called `jsconfig.json` and add the following code: 
```json
{
    "compilerOptions": {
        "paths": {
            "@/*": ["./src/*"]
        }
    }
}
```
> Finally, we can replace our `./` or `../` mapping nominclature with `@` instead which is now an alias to `/src/` directory. So now you can go to the `client/src/App.jsx` file and in the import statement replace `./` with `@` for the import to the Chat component. 
```js
import { useState } from "react"
import {BrowserRouter, Routes, Route, Navigate } from 'react-router-dom'
import Chat from '@/components/chat'
//...
```

7. Now if you have your vite server still running or if you have to start it up again (see Step 5f above) -- you can now nav in a browser to `http://localhost:5173/chat` and see the following: 
<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/233119946-ce7bef99-0faf-4855-ad6f-32ef9fa1bc4c.png">
</p>

##### [Back To The Top](https://github.com/rodriggj/chatgpt-app#build-process)
----------

## Chat Component - Front-End Initial Config

1. Nav back to the `client/src/components/chat/index.jsx` file. 

2. Add an import for the following Chat capabilities coming from Chat Engine 
- [ ] MultiChatLogic
- [ ] MultiChatSocket
- [ ] MultiChatWiindow

```js
import React from 'react'
import { useMultiChatLogic, MultiChatSocket, MultiChatWindow } from 'react-chat-engine-advanced'
//...
```

3. Now we need to add props to our component. We will make these props dynamic later for now for testing we will hard code our "user" and "password" from the user we created in the [Chat Engine Config](https://github.com/rodriggj/chatgpt-app#chat-engine-config) _Step 4_. We will also reference our env variables for our project id using the vite `import.meta.env` api. Add the following: 
```js
import React from 'react'
import { useMultiChatLogic, MultiChatSocket, MultiChatWindow } from 'react-chat-engine-advanced'

const Chat = () => {
    const chatProps = useMultiChatLogic(
        import.meta.env.VITE_PROJECT_ID,
        "rodriggj",
        "chatapp"
    )
//...
```

4. Finally we need to add some styling to the Chat component to take the full width of the entire window. So make the following modification to the `<div>` element. 
```js
//...
  return (
    <div style={{ flexBasis: "100%" }}>
      <p>Hello from the Chat component!</p>
    </div>
  )
//...
```

5. Next, replace our generic text placeholder with the _MultiChatSocket_ component and pass in our _chatProps_ as props to that component. Use destructuring to pass the props with the spread operator: 
```js
  return (
    <div style={{ flexBasis: "100%" }}>
      <MultiChatSocket {...chatProps}/>
    </div>
  )
```

6. Finally we need to configure the _MultiChatWindow_ component. We will again pass in a few props, style, and another component, a _Header_ which we will be able to customize later. 
```js
  return (
    <div style={{ flexBasis: "100%" }}>
      <MultiChatSocket {...chatProps}/>
      <MultiChatWindow {...chatProps} style={{ height: "100vh" }} renderChatHeader={ (chat) => <Header chat={chat}/>}/>
    </div>
  )
```

7. Now we need to create the Header component that we are referencing in the MultiChatWindow. To do this nav to `client/src/components` and create a new dir called `customHeader`. In this dir create another `index.jsx` file and then create the arrow function and export for our _Header_ component. 
```s
cd client/src/components
mkdir customHeader
code customHeader/index.jsx
```

```js
import React from 'react'

const Header = () => {
  return (
    <div>
      <p>Hello from inside Header component</p>
    </div>
  )
}

export default Header
```

You should now see a UI that looks like the following: 
<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/233136912-a5b6e4e6-03dd-44d0-87e7-2fcfb1bd3856.png">
</p>

##### [Back To The Top](https://github.com/rodriggj/chatgpt-app#build-process)

----------

## Header Component - Front-End Initial Config

1. Nav to the `client/src/components/customHeader` dir and open the index.jsx file. 

2. Add imports for icons we will use in the Header. The icons imported are coming from this library [heroicons](https://heroicons.com/)
```js
import React from 'react'
import { ChatBubbleLeftRightIcon, PhoneIcon } from '@heroicons/react/24/solid'
//...
```

3. Now we need to add the `chat` prop which we inherit from the chat component. Then we can parse the chat object into some divs tags to help organize our Header, and we will add classNames to refer to our CSS styling. Update the Header component with the following code: 
```js
//...
const Header = ({ chat }) => {
  return (
    <div className="chat-header">
        <div className="flexbetween">
            <ChatBubbleLeftRightIcon className="icon-chat"/>
            <h3 className="header-text">{chat.title}</h3>
        </div>
        <div className="flexbetween">
            <PhoneIcon className="icon-phone"/>
            <h3 className="header-text">{chat.description}</h3>
        </div>
    </div>
  )
}
//...
```

4. We can also remove `strict mode` on the `client/src/main.jsx` file. This will ensure that if the screen size is dynamically resizing that it will either produce the Chat window or "hamburger" icons. 
```js
ReactDOM.createRoot(document.getElementById('root')).render(
  <App />
)
```

##### [Back To The Top](https://github.com/rodriggj/chatgpt-app#build-process)

---------

## StandardMessageForm Component

1. Nav back to the `client/src/components/chat/index.jsx` file

2. Here we will write another function, `renderMessageForm`,  in our Chat component that will render a component we have not created yet called `StandardMessageForm`. 
```js
  return (
    <div style={{ flexBasis: "100%" }}>
      <MultiChatSocket {...chatProps}/>
      <MultiChatWindow {...chatProps} 
        style={{ height: "100vh" }} 
        renderChatHeader = { (chat) => <Header chat={chat}/>}
        renderMessageForm = { (props) => { return (
            <StandardMessageForm props={ props } activeChat={ chatProps.chat }/>
            ) 
        }}
        />
    </div>
  )
```

3. Now lets go create the `StandardMessageForm` component. First create the dir structure by creating a folder under `client/src/components` called `customMessageForms`. We will have several forms so create another sub-directory under `customMessageForms` and call it `StandardMessageForm`.  In that folder, create a `index.jsx` file. Input the following contents in the `index.jsx` file.
```js
import React from 'react'

const StandardMessageForm = () => {
  return (
    <div>
      <p>Hello from inside the Standard Message Form Component</p>
    </div>
  )
}

export default StandardMessageForm
```

4. Add the import statement to the `client/src/components/chat/index.jsx` file. 
```js
import React from 'react'
import { useMultiChatLogic, MultiChatSocket, MultiChatWindow } from 'react-chat-engine-advanced'
import Header from '@/components/customHeader'
import StandardMessageForm from '@/components/customMessageForms/StandardMessageForm'
//...
```

Now if you view the UI you should see that StandardMessageForm component render. 

<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/233195543-a2d9044e-4bc8-4f92-84d9-1b5813cfef81.png">
</p>

5. We need to create a message form that we display to the user. To do this we will create 2 components 1. a message container & 2. the message form where the user provides input. In the message container, I want to add a capability to display a preview icon of any attachments that are potentially included in the user input. To create the container and the preview capability input the following code in the `StandardMessageForm.jxs` file. 
```js
//...
const StandardMessageForm = () => {
  const [ message, setMessage ] = useState("")
  const [ attachment, setAttachment ] = useState("")
  const [ preview, setPreview ] = useState("")

  return (
    <div className="message-form-container">
      {preview && (
        <div className="message-form-preview">
          <img alt="message-form-preview" className="message-form-preview-image" src={ preview } onLoad={() => URL.revokeObjectURL(preview)}/>
          <XMarkIcon className="message-form-icon-x" onClick={() => {
            setPreview("")
            setAttachment("")
          }}/>
        </div>
      )}
      <div>Message Form goes here...</div>
    </div>
  )
}
//...
```

6. Now replace the `<div>` with the text "Message Form goes here ..." with the second component - the Message Form. 
```js
      <div className="message-form">
        <div className="message-form-input-container">
          <input className="message-form-input" type="text" value={message} onChange={ handleChange } placeholder="Send a message..."/>
        </div>
      </div>
```

7. Now we want to use a special react package called `DropZone` to allow a user to drop an image into our input form. `DropZone` will provide drag-drop capability and allow you to drag an image from a file system to our application. With the file uploaded the preview will populate as well. Enter the following code: 
```js
//...
          <Dropzone 
            acceptedFiles=".jpg,.jpeg,.png" 
            multiple={false} noClick={true} 
            onDrop={(acceptedFiles) => {
              setAttachment(acceptedFiles[0])
              setPreview(URL.createObjectURL(acceptedFiles[0]))
            }}>
            {({ getRootProps, getInputProps, open }) => (
              <div {...getRootProps()}>
                <input {...getInputProps()}/>
              </div>
            )}
          </Dropzone>
//...
```
The code above is effectively boilerplate code needed to get Dropzone to work. 

We can add customizations on top of the Dropzone capability for example here we can add an attachment icon from `React HeroIcons`. 
```js
//...
            {({ getRootProps, getInputProps, open }) => (
              <div {...getRootProps()}>
                <input {...getInputProps()}/>
                <PaperClipIcon className="message-form-icon-clip" onClick={open}/>
              </div>
            )}
//...
```

You should be able to see the following in your UI as a result. 

<p align="center">
<img width="350" alt="image" src="https://user-images.githubusercontent.com/8760590/233208731-5ff4213b-86a4-49e1-9d1c-4a4df90fd72a.png">
</p>

8. Finally we can add another icon to send the message and input some veritcal separator. Note the handleSumbit function is commented out and will be explained next. 
```js
          <hr className="vertical-line"/>
          <PaperAirplaneIcon 
            className="message-form-icon-airplane" 
            onClick={() => {
              setPreview("")
              // handleSumbit()
            }}/>
```

9. In order to to handle the submission of an attachment or message you have to create a handleSubmit function and add props to the StandardMessageForm. Populate the component with the following code: 
```js
const StandardMessageForm = ({props, activeChat}) => {
  const [ message, setMessage ] = useState("")
  const [ attachment, setAttachment ] = useState("")
  const [ preview, setPreview ] = useState("")

  const handleChange = (e) => {
    setMessage(e.target.value)
  }

  const handleSubmit = async () => {
    const date = new Date()
      .toISOString()
      .replace("T", " ")
      .replace("Z", `${Math.floor(Math.random() * 1000)}+00:00`)
    const at = attachment ? [{ blob: attachment, file: attachment.name }] : []
    const form = {
      attachments: at, 
      created: date, 
      sender_username: props.username, 
      text: message, 
      activeChatId: activeChat.id,
    }
    props.onSubmit(form)
    setMessage("")
    setAttachment("")
  }
  //...
  ```

Now that the handleSubmit function is written, you need to call the function onClick when the submit icon is pressed. 
```js
          <PaperAirplaneIcon 
            className="message-form-icon-airplane" 
            onClick={() => {
              setPreview("")
              handleSubmit()
            }}/>
```

##### [Back To The Top](https://github.com/rodriggj/chatgpt-app#build-process)

----------

## Initial Back End Configuration

1. Create a new folder at the same level of the `client` dir, called `server`, and change into the `server` dir. 

2. Run the following command to initiate a new project. 
```s
npm init -y
```

3. Create a `.env` file and input the following: 
```s
PORT=1337
OPEN_API_KEY=7d4a0a9d-bd39-4aa9-a2e2-01ee44fb65fd
```

4. Create a .gitignore file and input the following: 
```js
.env
node_modules
```

5. Now we need to install the dependencies packages. 
```js 
npm i express body-parser cors dotenv helmet morgan  --save
```

6. Now we need to modify the package.json file to be the following. Here we added "type" and "dev" nodes to the json file.
```json
{
  "name": "server",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "nodemon index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "body-parser": "^1.20.2",
    "cors": "^2.8.5",
    "dotenv": "^16.0.3",
    "express": "^4.18.2",
    "helmet": "^6.1.5",
    "morgan": "^1.10.0"
  }
}
```

7. Install nodemon package
```s
npm i -D nodemon
```

8. Now we need to create an `index.js` file within the `server` dir.
```js
code index.js
```

9. In the `index.js` file enter the following boilerplate code. 
```js
import express from 'express'
import bodyParser from 'body-parser'
import cors from 'cors'
import dotenv from 'dotenv'
import helmet from 'helmet'
import morgan from 'morgan'

/* Configuration */
dotenv.config()
const app = express()
app.use(express.json())
app.use(helmet())
app.use(helmet.crossOriginResourcePolicy({policy: "cross-origin"}))
app.use(morgan("common"))
app.use(bodyParser.json({limit:"30mb", extended: true}))
app.use(bodyParser.urlencoded({limit:"30mb", extended: true}))
app.use(cors())

/* Startup Server */
const PORT = process.env.PORT || 9000
app.listen(PORT, () => console.log(`Server is up and listening at http://localhost:${PORT}`))
```

10. From here we want to setup access to OpenAI. There is a github repo that explains how OpenAI wants the backend API incorporated into a Nodejs application, which can be found [here](https://github.com/openai/openai-node). The first thing we want to do is install the open.ai package. 

```s
npm i openai --save
```

11. Now from the `openai` github readme we can copy some boilerplate code and input into our express backend. 
```js
// from the github repository for OpenAI copy the following code
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
});
const openai = new OpenAIApi(configuration);
//...
```

And configure the index.js file to as follows
```js
import express from 'express'
import bodyParser from 'body-parser'
import cors from 'cors'
import dotenv from 'dotenv'
import helmet from 'helmet'
import morgan from 'morgan'
import { Configuration, OpenAIApi } from "openai"

/* Configuration */
dotenv.config()
const app = express()
app.use(express.json())
app.use(helmet())
app.use(helmet.crossOriginResourcePolicy({policy: "cross-origin"}))
app.use(morgan("common"))
app.use(bodyParser.json({limit:"30mb", extended: true}))
app.use(bodyParser.urlencoded({limit:"30mb", extended: true}))
app.use(cors())

/* Open AI Configuration */
const configuration = new Configuration({
  apiKey: process.env.OPEN_API_KEY
});
export const openai = new OpenAIApi(configuration);

/* Startup Server */
const PORT = process.env.PORT || 9000
app.listen(PORT, () => console.log(`Server is up and listening at http://localhost:${PORT}`))
```

> **NOTE:** Make sure the `process.env.`  reference is the same name as what is in the .env file.

##### [Back To The Top](https://github.com/rodriggj/chatgpt-app#build-process)

---------

## Configure Inital Back End Routes

1. Now that all this configuration is completed, we now need to configurea `routes` directory. In the `server` dir create a sub-dir called `routes`. 
```s
mkdir server/routes
```

2. Create a file to configure all the routes associated with calls to `openai` API. 
```s
cd server/routes
code openai.js
```

> **NOTE:** Typically Controllers are configured to deal with route handlers but for a prototype simplistic app, we will simply configure routes and not rout handlers. 

4. Here we are going to reference a package that will handle our API calls to Openai. So we need to install the axios node_module package in our package.json file, so lets do that now, and install axios. 
```s
npm i axios --save
```

5. Now in our `openai.js` file we can input the following boilerplate code. 
```js
import express from 'express'
import axios from 'axios'
import dotenv from 'dotenv'
import { openai } from '../index.js'

dotenv.config()
const router = express.Router()
```

4. Here we are going to reference a package that will handle our API calls to Openai. So we need to install the axios node_module package in our package.json file, so lets do that now, and install axios. 
```s
npm i axios --save
```

5. Create your first route here: 
```js
//...
router.post('/text', async(req, res) => {
    try {
        const { text, activeChatId } = req.body
    } catch (error) {
        res.status(500).json({ error: error.message })
    }
})
export default router
```

6. Now we need to connect our `openai` routes with our index.js file. To do so open the `server/index.js` file and enter the following code: 
```js

```

{{ finish documentation }}

##### [Back To The Top](https://github.com/rodriggj/chatgpt-app#build-process)

-----------

## Reference
- [ ] [Postman Collection](https://restless-sunset-487116.postman.co/workspace/ChatGPT-Workspace~339928bc-7f95-4a1c-8952-142b4d8196dc/collection/8708383-ab59f782-04b9-4c42-bb9b-47c2b0389379?action=share&creator=8708383)
- [ ] [NodeJS](https://nodejs.org/en/download/)
- [ ] [npx](https://www.npmjs.com/package/npx)
- [ ] [vite](https://vitejs.dev/guide/)
- [ ] [React Dropzone](https://react-dropzone.js.org/)
- [ ] [Redux](https://redux.js.org/)
- [ ] [Redux Toolki](https://redux-toolkit.js.org/)
- [ ] [Redux Toolkit Query](https://redux-toolkit.js.org/rtk-query/overview)
- [ ] [Hero Icons](https://heroicons.com/)
- [ ] [ChatEngine Docs](https://chatengine.io/docs/react/v2)
- [ ] [ChatEngine Storybook](https://chatengine-io.github.io/react-chat-engine-advanced/?path=/docs/multichatwindow--default-story)
- [ ] [ChatEngine Styling](https://chatengine.io/docs/react/v1/customize_ui/custom_css) 
- [ ] [Chat Engine API](https://rest.chatengine.io/)
- [ ] [Chat Engine](https://chatengine.io/)
- [ ] [OpenAI Completion Docs](https://platform.openai.com/docs/api-reference/completions/create) 
- [ ] [OpenAI Playground](https://platform.openai.com/playground)
- [ ] [OpenAI API ChatGPT Update](https://openai.com/blog/introducing-chatgpt-and-whisper-apis)
- [ ] [OpenAI Git Repo](https://github.com/openai/openai-node)
- [ ] [Ed Roh Git Repo](https://github.com/ed-roh/chat-app/blob/master/server/index.js)
- [ ] [YouTube Ref](https://www.youtube.com/watch?v=ffEDkqfIzxM)
--------
