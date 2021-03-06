# The method of packaging the native JavaScript google authorization login into a react component

## The react component(main code)
```react type="text/tsx"
import React, {useCallback, useLayoutEffect} from 'react';
import './App.css';

function App() {
  const initScript = () => {
    let script = document.createElement('script')
    script.type = 'text/javascript'
    script.async = true
    script.src = 'https://accounts.google.com/gsi/client'//这个代表的是script 的src
    script.onload = initGoogle
    document.head.appendChild(script)
  }
  useLayoutEffect(() => {
    initScript()
  }, [])
  const initGoogle = useCallback(() => {
    //@ts-ignore
    if (typeof window.google === 'undefined') {
      console.log('google is undefined')
    } else {
      console.log('google is defined')
      //@ts-ignore
      // console.log('useEffect',window.google)
      //@ts-ignore
      window.google?.accounts?.id.initialize({
        client_id: "559756290278-9v1ngbvivap03i80qntgsin48ggmj5pc.apps.googleusercontent.com",
        login_uri: "https://metaplasia.io",
        ux_mode: "popup",
        context: "signin",
        callback: function (e: any){
          console.log(e)
        }
      });
      //@ts-ignore
      window.google?.accounts?.id.renderButton(
          document.getElementById("buttonDiv"),
          { theme: "filled_black", size: "large",shape: "circle" }  // customization attributes
      );
      //@ts-ignore
      window.google?.accounts?.id.prompt(); // also display the One Tap dialog
    }
  }, [])
  return (
    <div className="App">
      <header className="App-header">
        <div id="buttonDiv"/>
      </header>
    </div>
  );
}

export default App;

```
## about google sign in（react encapsulates google authorization login）

Sign In With Google JavaScript API reference [google sign in](https://developers.google.com/identity/sign-in/web/reference)

## about creat react app

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).


