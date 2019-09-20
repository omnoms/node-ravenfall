# node-ravenfall

Example usage:

Initializing the client...
```js
const config = {
    baseUrl: "https://www.ravenfall.stream/api/",
    username:"myravenfallusername",
    password: "myravenfallpassword",
    debug: false
}
const Ravenfall = require('./ravenfall');
var r = new Ravenfall(config);
```

Using the ravenfall client examples;

Getting the currently available items and their descriptions (and stores them internally in the ravenfall client for re-use)
```js
r.GetItems().catch(function(err) {
    console.log("ERR GetItems:" + err);
});
```

Getting player stats and showing the current level + progression (similar to the official !stats)
```js
r.GetPlayerByTwitchId(chatter.user_id).then(function(data) { 
    var stats = [];
    if(typeof data !== "undefined" && typeof data.skills !== "undefined") {
        for(var s in data.skills) {
            if(s!== "id" && s !== "revision") {
                var item = data.skills[s];
                stats.push(s + " " + r.ExperienceToLevel(item) + " (" + r.Progress(item) + ")");    
            }
        }    
    }
    console.log(stats.join(", "));
}).catch(function(err) {
    console.log("ERR GetPlayerByTwitchId:" + err);
});            
```
