# Lithic Technical Support Lead - Hidden Challenge Solution

## 🔍 How I Found It
While reviewing the job description for the Technical Support Lead position on Greenhouse, I decided to inspect the source code of the application. I noticed that the anchor link wrapping the term **"problem-solving"** in the *"What You'll Bring"* section had a long, non-standard URL. Rather than pointing to an external domain, the `href` attribute contained a raw, Base64-encoded string.

## 💻 How I Decoded It
I extracted the Base64 string and decoded it using Python:

```bash
echo "IyEvdXNy..." | base64 --decode > puzzle.py
```

The decoded file revealed a Python script containing instructions to solve the hidden challenge, run the puzzle, and document my steps here.

## ⚙️ Running the Script
To verify the encryption and generate my candidate-specific proof code, I ran the Python script with my full name:

```bash
DONT_PANIC=1 python3 puzzle.py --candidate "Stephen Skalamera"
```

### Exact Output Received:
```text
Decrypted password: 42
Candidate: Stephen Skalamera
Proof code: cc1928e9e3cf
```

## 🧠 What This Script Does
The script decrypts an internal passphrase (`"42"`) using a simple, hardcoded bitwise XOR logic:
`bytes(a ^ b for a, b in zip(password, _key))`

Once the answer (`"42"`) is decrypted, the script normalizes the candidate's name to lowercase and generates a 12-character SHA-256 validation hash:
`hashlib.sha256(f"{normalized_name}:{answer}:so-long-and-thanks".encode()).hexdigest()[:12]`

## 🛠️ Tools Used
* **Python 3.11** for decoding and script execution.
* **Gemini to analyze the page source
