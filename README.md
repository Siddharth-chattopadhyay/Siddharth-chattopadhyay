I mostly do experiments with ideas in my head and use any language I have knowledge about, like C++, bash or JavaScript. I also do other experiments like network ports (default HTTP port is 80), with termux, ADB and Cryptography. However, I have not mastered everything fully and still in learning journey (like learning about different APIs of that language.).

Here's the experiments below:
```js
// It's incomplete
const childProcess = require("child_process");

class TermuxSensor {
    callbacks = [];
    constructor(sensors, delay = 2) {
        this.sensor = childProcess.spawn("termux-sensor", ['-d', delay, '-s', sensors]);

        this.sensor.on("spawn", () => {
            this.sensor.stdout.on("data", (chunk) => {
                for (const callback of this.callbacks)
                    callback(chunk);
            });
        });
    }

    addEventListener(callback) {
        this.callbacks.push(callback);
    }

    killProcess() {
        this.sensor.kill();
    }
};

const http = require("http");
const PORT = 80; // This is the default port for HTTP
const server = http.createServer((req, res) => {
});

const listened = server.listen(PORT);

listened.on("listening", () => {
    console.log('Server is listening at http://127.0.0.1');
});
```
