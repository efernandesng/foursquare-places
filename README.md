# Summary

framework agnostic javascript wrapper for foursquare's APIs

## Tests

yarn or npm `yarn test`

## Commit Policy

please test any functions added and put the tests in the `/tests` folder

## React Example

Here is a simple react application:

1. Setup React Project

`npx create-react-app mr-jitters`

2. Install Package

`cd mr-jitters`

`npm install -i @foursquare/foursquare-places`

3. Create ./.env file and add CLIENT_ID and CLIENT_SECRET

```
REACT_APP_CLIENT_ID=InsertClientId
REACT_APP_CLIENT_SECRET=InsertClientSecret
```

4. Add Env file to .gitignore

```
# env
.env
```

5. Modify your src/App.js

```
import React, { useState, useEffect } from "react";
import Foursquare from "@foursquare/foursquare-places";

// need to create an .env file - see instructions in link
// https://stackoverflow.com/questions/48699820/how-do-i-hide-api-key-in-create-react-app
const CLIENT_ID = process.env.REACT_APP_CLIENT_ID;
const CLIENT_SECRET = process.env.REACT_APP_CLIENT_SECRET;
const foursquare = new Foursquare(CLIENT_ID, CLIENT_SECRET);

const App = () => {
  const [items, setItems] = useState([]);
  const [params, setParams] = useState({
    ll: "37.7749,-122.4194",
    query: "Blue Bottle"
  });

  useEffect(() => {
    foursquare.venues.getVenues(params).then(res => {
      setItems(res.response.venues);
    });
  }, [params]);

  return (
    <div>
      <div>Items:</div>
      {items.map(({ id, name }) => (
        <div key={id}>{name}</div>
      ))}
    </div>
  );
};

export default App;
```

6. Start your React App

`npm start`
