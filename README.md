# React Fetch Data with Hooks

```
/**
 * -----------
 * FETCH DATA
 * -----------
 * I'm using my github profile to fetch data from
 * @link https://api.github.com/users/m-soro
 * Fetch data using a combination of useState and useEffect
 * Regardless of any data:
 * First Step is to fetch using useState and useEffect combination
 * Second is use React to pass properties down to a child component
 */

// Another component
function GithubUser({ name, location, avatar }) {
  return (
    <div className="GithubUser">
      <h1>{name}</h1>
      <p>{location}</p>
      <img
        src={avatar}
        alt={name}
        style={{ height: "150px", borderRadius: "50%" }}
      />
    </div>
  );
}

import "./App.css";
import { useState, useEffect } from "react";

// useState to handle the data
// useEffect to make the call for the external data
function App() {
  let url = "https://api.github.com/users/m-soro";
  // create container for the data
  const [data, setData] = useState(null);
  // call the api
  useEffect(() => {
    // fetch is built into the browser. A way of making http request to get data from a source
    // once we get the data take that response and call .json() to turn it into json
    fetch(url)
      .then((response) => response.json())
      // then passs this json data to our data container
      .then(setData);
    // pass an empty array to tell useEffect to only get data once
  }, []);
  // if data has a value, display it in GithubUser component
  if (data) {
    return (
      <GithubUser
        name={data.name}
        location={data.location}
        avatar={data.avatar_url}
      />
    );
  }

  return (
    <div className="App container">
      <h2>Fetch data with hooks</h2>
    </div>
  );
}

export default App;

```
