<!-- TITLE: 2019 EV -->
<!-- SUBTITLE: Designs and logs of the 2019 electric car -->

# Subsystems
Chassis
Suspension

## Code
Code for asynchronously rolling dice

```js
module.exports = async function (input) {
    return new Promise((resolve, reject) => {
        var str = input.split(' ');
        var i, val, dice;
        for (i = 0; i < str.length; i++) {
            val = str[i];
            if (val.substring(0).match(/\dd\d/)) {
                dice = val;
                break;
            }
        }

        if (dice === undefined) {
            var msg = 'Please follow the actual syntax.';
            return reject(msg);
        }

        var numDice = parseInt(dice.split('d')[0]);
        var diceType = parseInt(dice.split('d')[1]);

        if (diceType != 4 && diceType != 6 && diceType != 8 && diceType != 10 && diceType != 12 && diceType != 20) {
            var msg = 'That is not a standard die.';
            return reject(msg);
        } else {
            let min = Math.ceil(numDice);
            let max = Math.floor(numDice * diceType);
            let num = Math.floor(Math.random() * (max - min + 1) + min);
            console.log(`Rolled: ${num}`);
            return resolve(num.toString());
        }

    });
}
```

## Code 2
Code for flipping someone off

```js
const axios = require('axios');

async function fuckoff(user) {
    return new Promise((resolve, reject) => {
        const fuckoffs = ['asshole', 'bag', 'bucket', 'bye', 'cool', 'cup', 'family', 'fascinating', 'flying', 'fyyff', 'give', 'horse', 'immensity', 'looking', 'no', 'ratsares', 'shit', 'single', 'thanks', 'that', 'this', 'too', 'what', 'zero'];
        let endpoint = fuckoffs[Math.floor(Math.random() * fuckoffs.length)];
        axios({
            method: 'get',
            url: `https://www.foaas.com/${endpoint}/${user}`,
            headers: {
                'Accept': 'application/json'
            }
        }).then(res => {
            console.log(res.data);
            const msg = [{
                    "type": "section",
                    "text": {
                        "type": "mrkdwn",
                        "text": res.data.message
                    }
                },
                {
                    "type": "context",
                    "elements": [{
                        "type": "mrkdwn",
                        "text": res.data.subtitle
                    }]
                }
            ];
            return resolve(msg);
        }).catch(console.error);
    });
}

async function fuckall(user) {
    return new Promise((resolve, reject) => {
        const fuckalls = ['everyone', 'everything'];
        let endpoint = fuckalls[Math.floor(Math.random() * fuckalls.length)];
        axios({
            method: 'get',
            url: `https://foaas.com/${endpoint}/${user}`,
            headers: {
                'Accept': 'application/json'
            }
        }).then(res => {
            console.log(res.data);
            const msg = [{
                    "type": "section",
                    "text": {
                        "type": "mrkdwn",
                        "text": res.data.message
                    }
                },
                {
                    "type": "context",
                    "elements": [{
                        "type": "mrkdwn",
                        "text": res.data.subtitle
                    }]
                }
            ];
            return resolve(msg);
        }).catch(console.error);
    })
}

module.exports = {
    fuckoff,
    fuckall
}
```