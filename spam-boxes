const sleep = (ms) => new Promise(r => setTimeout(r, ms));

(async () => {
    const box = prompt('What box do you want to open? (EXAMPLE: Space)');
    const amount = prompt('How many boxes do you want to open?');

    const response = await fetch('https://api.blooket.com/api/users/verify-token', {
        method: "GET",
        headers: {
            "accept": "application/json, text/plain, */*",
            "accept-language": "en-US,en;q=0.9,ru;q=0.8",
        },
        credentials: "include"
    });
    const data = await response.json();

    (new Promise(async (resolve, reject) => {
        var blooks = [];

        for (let i = 0; i < amount; i++) {
            await sleep(500);
            fetch('https://api.blooket.com/api/users/unlockblook', {
                method: "PUT",
                headers: {
                    "accept": "application/json, text/plain, */*",
                    "accept-language": "en-US,en;q=0.9,ru;q=0.8",
                },
                credentials: "include",
                body: JSON.stringify({
                    box: box,
                    name: data.name,
                }),
            }).then(r => r.json()).then(r => blooks.push(r.unlockedBlook));
        };

        resolve(blooks);

    })).then(blooks => {
        let count = {};

        blooks.forEach((i) => count[i] = (count[i] || 0) + 1);
        
        alert(`Results:\n` + Object.entries(count).map((x) => `    ${x[1]} ${x[0]}`).join(`\n`));
    });
})();
