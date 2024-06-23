- 👋 Hi, I’m @tylerggf
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
tylerggf/tylerggf is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
// Aimbot
(function() {
    let oldSend = WebSocket.prototype.send;
    WebSocket.prototype.send = function(data) {
        if (data.includes("pos") && data.includes("rot")) {
            let newData = JSON.parse(data);
            let target = { x: newData.pos.x + 100, y: newData.pos.y + 100 };
            let deltaX = target.x - newData.pos.x;
            let deltaY = target.y - newData.pos.y;
            let angle = Math.atan2(deltaY, deltaX);
            newData.rot = angle * (180 / Math.PI);
            data = JSON.stringify(newData);
        }
        oldSend.apply(this, [data]);
    };
})();

// Wallhack
(function() {
    let oldSend = WebSocket.prototype.send;
    WebSocket.prototype.send = function(data) {
        if (data.includes("ray") && data.includes("shoot")) {
            let newData = JSON.parse(data);
            newData.ray.hit = true;
            data = JSON.stringify(newData);
        }
        oldSend.apply(this, [data]);
    };
})();

// Instant Reload
(function() {
    let oldSend = WebSocket.prototype.send;
    WebSocket.prototype.send = function(data) {
        if (data.includes("reload")) {
            let newData = JSON.parse(data);
            newData.reload = true;
            data = JSON.stringify(newData);
        }
        oldSend.apply(this, [data]);
    };
})();
