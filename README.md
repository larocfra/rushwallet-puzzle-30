# 🔍 RushWallet Puzzle #30 — Community Investigation

> **29 of 30 wallets claimed. I have documented 26 passphrases. Help find the missing ones.**

---

## 💰 The Prize

| | |
|---|---|
| **Address** | `13Q8hJqagtd77ojTJcEZPjTz2sBFSsYxyj` |
| **Balance** | 0.01 BTC (unclaimed since April 2015) |
| **Current value** | ~$728.47 USD |
| **Contest** | KryptoKit 2014 — 30 brainwallets hidden in a promotional video |

> This wallet has been sitting unclaimed for over 10 years. With BTC's rise in value, it's now worth real money.

---

## 📖 Background

In late 2014, the team behind [KryptoKit](https://kryptokit.com) and [RushWallet](https://rushwallet.com) hid **30 Bitcoin brainwallets** inside a promotional video as a contest. Passphrases were encoded in the video as visible text, subliminal flashes, repeated phrases, and other tricks — and some were hidden in the **KryptoKit website source code**.

**29 wallets have been claimed on the blockchain. We have documented 25 passphrases. 3 were claimed but the passphrase was never shared publicly. Wallet #30 has never been claimed.**

This repo documents everything found so far with annotated frames so the community can help crack what's left.

---

## 🎬 The Video

The puzzle uses a short promotional video featuring a character named "Dmitri" who tells a story about his colleague Enrique's noisy keyboard.

> **Important:** YouTube re-encoding destroyed the subliminal text. The original archived version at the Wayback Machine is the only reliable source for frame analysis.

- **Archive version** (`video/` folder or Releases) — 1280×720, 1027 kb/s, created 2014-12-28
- **YouTube HD** — 2560×1440 but subliminal text is degraded and unreliable

<details>
<summary>📄 Full video transcript</summary>

> "This is me. My name is Dmitri and i like-a the Bitcoin. I want to tell you a little story about my friend from work, Enrique. Every day I come in office and Enrique is pushing all the buttons on his old keyboard. It's so loud. Everybody in the office hate him for this. Every night I can hear it in my sleep. It give me nightmare. But the one night I was hearing about this website Rushwallet. They say I can make a fundraiser. So I go on a www.rushwallet.com and I move my finger on the screen and I make a Bitcoin wallet. From there I create a fundraiser for new quiet keyboard, and I send it to all the peoples in the office. In only 15 minutes we were able to buy him the quietest keyboard on the Internets. And now I have no more nightmares. I sleep like a princess. And the best part, Rushwallet took none of my money, because they have a no fees and they don't hold any of my bitcoins. You can use Rushwallet for anything. For example, Nancy used Rushwallet fundraiser to pool money together for her boyfriend's birthday. They ended up getting him 3d printer. Now he's the coolest guy on the block. Or how 'bout Jason Kings? He's raising money right now to help homelessness. He's turning thrift shop into a Bitcoin homeless center. What a good gentlemans! Maybe you make a fundraiser for charity, or maybe you want to buy babooshka a new coat. You can use Rushwallet fundraiser for anything. What will you use it for? Hello-ah, it is me again! Did you see all the clues? I hid the bitcoins in many brain wallets in the video. If you want to win the bitcoins, go to rushwallet.com/contest and make a guess. Good luck."

</details>

---

## 🕵️ How Clues Were Hidden

Clues were embedded in **three different ways:**

### 1. Visible text in video frames
Text visible on screen — banners, table legs, balloons, posters, wall objects.

### 2. Subliminal flashes
Faint text embedded in specific frames, only visible in the archive version. Pattern:
```
[TEXT]  X[N]
```
`X[N]` means repeat the text `N` times to form the passphrase.

| Frame region | Subliminal text | Full passphrase |
|---|---|---|
| Coins during dancing scene | `5784623964023 X2` | `5784623964023 5784623964023` |
| Dancing scene | `supercalifragilisticexpialidocious X3` | `supercalifragilisticexpialidocious` × 3 |
| Bus scene (frames 2054–2058) | `DID YOU SEE THIS X7` | *(RushWallet 2 clue — not wallet #30)* |

### 3. KryptoKit website source code
Some passphrases were hidden on the `kryptokit.com` website itself — either as visible page text or embedded in the HTML source code (press F12 on the archived page).

- **Wallet #5**: `Bitcoin wallet and tools built right into your browser.` — KryptoKit homepage tagline
- **Wallet #14**: `the kryptokit hardware wallet is coming soon` — hidden in HTML source as ASCII art with a Dmitri speech bubble

> Always check the Wayback Machine snapshot of `kryptokit.com` from late 2014 for hidden text.

---

## 🗂️ This Repo

```
found/          ← Annotated frames for each documented wallet (numbered markers)
video/          ← Original archive video (see Releases for full frame zip)
findings.md     ← Full wallet list, open leads, and eliminated candidates
```

The `found/` folder contains annotated screenshots from the video with numbered markers showing exactly where each clue appears. Website source clues are also documented there.

---

## 🆘 Where We Need Help

### Wallets #13, #23, #26 — Claimed but passphrase unknown
These three were claimed during the original 2014–2015 contest but the passphrases were **never publicly shared**. We don't know how they were solved. If you were around in 2014 and remember, or if you can find references on Bitcointalk or elsewhere, please open an issue!

### 🔥 Wallet #30 — Never claimed
The last wallet has never been swept. Active leads:

| Lead | Description |
|---|---|
| **16 coins (frame ~01575)** | A crowned dancing woman surrounded by exactly 16 Bitcoin coins. Subliminal text on the coins has not been read clearly yet — same technique as `5784623964023 X2`. |
| **Blue rectangle on wall** | Appears in the office/living room scene. May contain faint hidden text only readable in the full archive version. |

See `findings.md` for the full list of what's already been eliminated.

---

## 🔑 How Brainwallets Work

All 30 wallets use the same formula — SHA-256 hash of the passphrase → **uncompressed** Bitcoin address:

```python
import hashlib, ecdsa, base58

def brainwallet(phrase):
    priv = hashlib.sha256(phrase.encode('utf-8')).digest()
    sk = ecdsa.SigningKey.from_string(priv, curve=ecdsa.SECP256k1)
    vk = sk.get_verifying_key()
    x = vk.pubkey.point.x()
    y = vk.pubkey.point.y()
    pub = b'\x04' + x.to_bytes(32, 'big') + y.to_bytes(32, 'big')  # UNCOMPRESSED
    sha = hashlib.sha256(pub).digest()
    rip = hashlib.new('ripemd160')
    rip.update(sha)
    h = b'\x00' + rip.digest()
    chk = hashlib.sha256(hashlib.sha256(h).digest()).digest()[:4]
    return base58.b58encode(h + chk).decode()
```

> ⚠️ **Must use uncompressed keys.** Compressed keys generate a different address.

---

## 🤝 How to Contribute

- **Open an issue** with a candidate passphrase and what clue it comes from
- **Submit a PR** adding findings to `findings.md`
- **Share a Wayback snapshot** of `kryptokit.com` from 2014 if you find one
- **Enhance the frames** — if you have image processing skills, try sharpening the unsolved coin frames

Please check `findings.md` first to avoid testing already-eliminated candidates.

---

## 📎 References

- [Wayback Machine — KryptoKit](https://web.archive.org/web/2014*/kryptokit.com)
- [Bitcoin address on blockchain explorer](https://www.blockchain.com/explorer/addresses/btc/13Q8hJqagtd77ojTJcEZPjTz2sBFSsYxyj)

---

*Investigation ongoing since 2015 · Last updated April 2026*
