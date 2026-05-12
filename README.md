//
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
const PORT = 32765;
const server = http.createServer((req, res) => {
});

const listened = server.listen(PORT);

listened.on("listening", () => {
    console.log('Server is listening at http://localhost:' + PORT);
});
