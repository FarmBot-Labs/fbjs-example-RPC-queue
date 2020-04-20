# How Do I Execute `execSequence` Sequentially?

**ANSER:** Use Javascript Promise objects.

# Example of Promise Usage with `execSequence`

```javascript
global.atob = require("atob");
const { Farmbot } = require("farmbot");
const axios = require("axios");

const password = "password";
const email = "email@address.com";
const SERVER = "https://my.farm.bot";
const SEQUENCE1 = 123;
const SEQUENCE2 = 123;
let farmbot = null;

axios
  .post(SERVER + "/api/tokens", { user: { email, password } })
  .then(response => response.data.token.encoded)
  .then((token) => {
    farmbot = new Farmbot({ token: token });
    return farmbot.connect();
  })
  .then(() => farmbot.execSequence(SEQUENCE1)) // <= This is critical!
  .then(() => farmbot.execSequence(SEQUENCE2)) // <= This is critical!
  .catch(error => console.dir(error));
```
