# ChatGPT-Clone
![alt text](https://github.com/PratyayMallik1006/ChatGPT-Clone/blob/main/screenshots/ss1.PNG?raw=true)
![alt text](https://github.com/PratyayMallik1006/ChatGPT-Clone/blob/main/screenshots/ss2.PNG?raw=true)
![alt text](https://github.com/PratyayMallik1006/ChatGPT-Clone/blob/main/screenshots/ss3.PNG?raw=true)
# Running Application
- Frontend:
```
npm run start:frontend
```
- Backend:
```
npm run start:backend
```

# Notes
## Using ChatGPT API
1. Genereating API Key : https://platform.openai.com/account/api-keys
2. Posting request
- backend
```js
const API_KEY = "APIKEY";

app.post("/completions", async (req, res) => {
  const options = {
    method: "POST",
    headers: {
      Authorization: `Bearer ${API_KEY}`,
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      model: "gpt-3.5-turbo",
      messages: [{ role: "user", content: req.body.message }],
      max_tokens: 100,
    }),
  };
  try {
    const response = await fetch(
      "https://api.openai.com/v1/chat/completions",
      options
    );
    const data = await response.json();
    res.send(data);
  } catch (error) {
    console.error(error);
  }
});
```
- frontend
```js
const getMessages = async () => {
    const options = {
      method: "POST",
      body: JSON.stringify({
        message: "Tell me an AI joke",
      }),
      headers: {
        "Content-Type": "application/json",
      },
    };
    console.log("Submit Button pressed");
    try {
      const response = await fetch(
        "http://localhost:8000/completions",
        options
      );
      const data = await response.json();
      response = data.choices[0].message;
    } catch (error) {
      console.error(error);
    }
  };
```
