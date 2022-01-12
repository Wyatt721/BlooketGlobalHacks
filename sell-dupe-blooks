async function getName() {
    const response = await fetch('https://api.blooket.com/api/users/verify-token', {
        method: "GET",
        headers: {
            "accept": "application/json, text/plain, */*",
            "accept-language": "en-US,en;q=0.9,ru;q=0.8",
        },
        credentials: "include"
    });
    const data = await response.json();

    return data.name;
};


async function getBlooks(blooketName) {
    const response = await fetch('https://api.blooket.com/api/users/blooks?name=' + blooketName, {
        headers: {
            "accept": "application/json, text/plain, */*",
            "accept-language": "en-US,en;q=0.9,ru;q=0.8",
        },
        credentials: "include"
    });
    const data = await response.json();

    return data;
};

async function sellDupeBlooks() {
    const blooks = await getBlooks(await getName());
    const x = Object.entries(blooks).filter(i => i[1] > 1).map(i => [i[0], i[1] - 1]);

    for (const [blook, val] of x) {
        await fetch('https://api.blooket.com/api/users/sellblook', {
            method: "PUT",
            headers: {
                "referer": "https://www.blooket.com/",
                "content-type": "application/json",
            },
            credentials: "include",
            body: JSON.stringify({
                blook: blook,
                name: await getName(),
                numSold: val
            }),
        });
    }

    if (x.length > 0) {
        alert('Results:\n' + x.map(x => `    ${x[1]} ${x[0]}`).join('\n'));
    } else {
        alert("No duplicate Blooks found.");
    };

};

sellDupeBlooks();
