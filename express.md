# ExpressJS

21 Dec 2020

`Express` is a NodeJS library that allows you to create a server using JavaScript (doesn't need to be run in a browser). `Nodemon` is a command-line tool that helps with development of Node applications (it monitors and restarts your app when it detects changes.)

## Setup

Create folder structure normally, or with command-line: (may need to use GitBash on windows):

- Create a folder with for your project e.g. `mkdir express-demo`
- Create frontend and backend folders `cd express-demo`, `mkdir frontend backend` (could use `client` and `server` folder names)
- Create index html file in frontend `cd ../frontend`, `touch index.html`
- Go to backend and init an NPM project `cd ../backend`, `npm init -y` (`-y` flag just says yes to all the default options in one go and gives you a default `package.json`)
- Create an index.js file in the backend folder `touch index.js` and paste in example code from [https://expressjs.com/en/starter/hello-world.html](https://expressjs.com/en/starter/hello-world.html)
- Unstall Express and Nodemon in the backend folder `npm install express nodemon`
- Create dev script for running the server - in scripts section of `package.json`, add `"dev": "nodemon index.js"`
- you will now be able to run the server with: `npm run dev`

## Creating an endpoint

- The port number is where the server will listen on - change it to `const port = 4444;` etc.
- run the server with `npm run dev` and go to `http://localhost:4444` in the browser, you should now see `hello world`
- add `app.use(express.json());` at the top of the `index.js` file, before `app.get(...)`
- make a new post endpoint below `app.get(...)`:
  ```
  app.post('/', (req, res) => {
    const { mykey } = req.body;
    console.log(`this is a post endpoint. This is the key: ${mykey}`);
    res.json({
      myresult: 'Hello World',
      mykey: mykey,
    });
  });
  ```

### Testing with Postman

- To test API endpoints we can use [Postman](https://www.postman.com/), install and sign-up
- At the top-left you can make a new `workspace` e.g. `Bath Spa` and underneath you can make a `collection` e.g. `express demo endpoints` - these allow you store different endpoint tests etc.
- In the middle panel make a new reques with type `POST` and url `localhost:4444`
- Underneath that select `Body` and `raw` with type dropdown set to `JSON`
- in the panel below write the JSON that will be sent to the endpoint
  ```
  {
    "mykey": "XYZ"
  }
  ```
- Press Send and it should return the JSON response:
  ```
  {
    "myresult": "Hello World",
    "mykey": "XYZ"
  }
  ```
- Press Save to save the request and add it to the collection in Postman

### Testing with HTML

- Go to the `frontend/index.html` (can open up a separate VScode with the `frontend` folder)
- Put in some dummy text for the webpage:
  ```
  <h1>This is the front end</h1>
  <p>
    Lorem, ipsum dolor sit amet consectetur adipisicing elit. Repellat, minus
    vero fuga non nam ipsa iure est? Facilis, enim incidunt!
  </p>
  ```
- In the body, add this script (copied and edited from [MDN Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch):

  ```
  <script crossorigin>
    // Example POST method implementation:
    async function postData(url = '', data = {}) {
      // Default options are marked with *
      const response = await fetch(url, {
        method: 'POST', // *GET, POST, PUT, DELETE, etc.
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(data), // body data type must match "Content-Type" header
      });
      return response.json(); // parses JSON response into native JavaScript objects
    }

    postData('http://localhost:4444', { mykey: 'XYZ' }).then((data) => {
      console.log(data); // JSON data parsed by `data.json()` call
    });
  </script>
  ```

- This still probably wont work yet because of `CORS` errors - [Cross-Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/Errors)
- Back in the `backend` folder, install Cors `npm install cors`
- In `backend/index.js` add `const cors = require('cors');` at the top, and `app.use(cors());` underneath
- Open up `index.html` with LiveServer (May need to open the `frontend` folder in VSCode first - it should open as `localhost:5501/index.html` etc. otherwise would be `localhost:5501/frontend/index.html` from the main `express-demo` folder)
- In the webpage console you should now see the response being logged:
  ```
  {myresult: 'Hello World', mykey: 'XYZ'}
  ```

## Notes:

- The frontend (LiveServer) and the backend (Express) have different ports as we are essentially simulating both the client and the server on our localhost
- As we create the NPM package in the `express-demo/backend` folder, make sure to install the packages and run the server from that filepath
- An alternative to using `app.use(express.json())` is the NPM package `body-parser` (probably has much more things it can do, but more complicated??)
- If you need to install stuff while you still have the server running, you can open up another terminal. Or if you need to close the server you can press `CTRL + C` in the terminal, install what you need, then start the server back up again.
