# gpt4-reverse-proxy
GPT4が使いたいけど高すぎる! そんなあなたへ! gpt4-reverse-proxy!!


Chat SmithというiOSのアプリがあるのですがそこでGPT-4の抜け穴を発見!
更にいろいろ偽造しスマホでリクエストしてるかのように勘違いさしてAPIにしちゃいました!!

↑テンションおかしいのは気にしちゃだめですよ()


アホなのがこのコードChat Smithがほとんど書いてくれたんだよ?
自分で自分の脆弱性を言う素晴らしいAI (OpenAIのAPIだから)


sample
```js
const fetch = require("node-fetch")

async function main() {
    let messages = []
    messages.push({
        content: [
            { "type": "text", "text": "what is this?" },
            { "type": "image_url", "image_url": { "url": "https://upload.wikimedia.org/wikipedia/commons/thumb/0/04/ChatGPT_logo.svg/512px-ChatGPT_logo.svg.png"} }
        ],
        role: "user"
    })

    const res = await fetch(`http://127.0.0.1:35803/generate`, {
        method: "POST",
        headers: {
            'Content-Type': 'application/json',
            "accept-language": "en-US,en;q=0.9",
        },
        body: JSON.stringify({ messages })
    })

    if (!res.ok) return;

    console.log(await res.text())
    const json_res = await res.json();
    console.log(json_res)
}


main()
```