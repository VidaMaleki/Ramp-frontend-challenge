# Ramp Challenge Solution

This repository contains my solution for Ramp's frontend CTF-style challenge.

## 🧩 About the Challenge

I was tasked with:
- Decoding a Base64 string to reveal the challenge instructions.
- Analyzing the DOM to extract a hidden URL following a custom pattern.
- Fetching a flag from that URL.
- Building a React app to display the flag with a typewriter animation — without using any external libraries.

It was a fun and thoughtful challenge, blending DOM manipulation, React frontend logic, and problem-solving!

---

## 🛠 How I Solved It

### Step 1: Decode the Base64 URL

The given Base64 string:

aHR0cHM6Ly90bnM0bHBnbXppaXlwbnh4emVsNXNzNW55dTBuZnRvbC5sYW1iZGEtdXJsLnVzLWVhc3QtMS5vbi5hd3MvcmFtcC1jaGFsbGVuZ2UtaW5zdHJ1Y3Rpb25zLw==

Decoded to:

https://tns4lpgmziiypnxxzel5ss5nyu0nftol.lambda-url.us-east-1.on.aws/ramp-challenge-instructions/

---

### Step 2: Find the Hidden URL in the HTML

After visiting the challenge page, I extracted the hidden URL using this script in the browser DevTools console:

```javascript
const flagChars = [];

document.querySelectorAll('section[data-id^="92"]').forEach(section => {
  const article = section.querySelector('article[data-class$="45"]');
  if (!article) return;

  const div = article.querySelector('div[data-tag*="78"]');
  if (!div) return;

  const charElement = div.querySelector('b.ref');
  if (charElement) {
    const char = charElement.getAttribute('value');
    if (char) flagChars.push(char);
  }
});

const flagUrl = flagChars.join('');
console.log("✅ Hidden flag URL:", flagUrl);
```

Result:
`https://wgg522pwivhvi5gqsn675gth3q0otdja.lambda-url.us-east-1.on.aws/6f7263`
The word revealed was: `orchids`

### Step 3: Build the React Application
I created a simple React app that:

Fetches the hidden flag.

- Fetches the hidden flag.

- Shows a "Loading..." message while fetching.

- Displays each character of the flag one by one with a 500ms delay (typewriter animation).

- Uses only React APIs — no external libraries or CSS animations.

#### 🔗 CodeSandbox Demo:
`https://codesandbox.io/p/sandbox/ramp-challenge-n76msc?file=%2Fsrc%2FApp.tsx%3A1%2C1-90%2C1`
#### 🔗 Hidden URL (result):
`https://wgg522pwivhvi5gqsn675gth3q0otdja.lambda-url.us-east-1.on.aws/6f7263`

The word revealed was:
`"orchids"`


### Final Thoughts
Honestly, this Ramp challenge was an amazing experience:

- I decoded a hidden instruction set.

- Parsed the DOM with precision to extract the URL.

- Troubleshooted React Strict Mode double-render issues.

- Fine-tuned the animation for a smooth user experience.

- It combined frontend engineering, problem-solving, debugging, and creativity — the kind of work I love! 
