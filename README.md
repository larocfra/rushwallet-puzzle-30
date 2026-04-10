# 🔍 RushWallet Puzzle #30 — Community Investigation

> **24 of 30 brainwallets solved. 6 remain. Help us find the last ones.**

---

## 💰 The Prize

| | |
|---|---|
| **Address** | `13Q8hJqagtd77ojTJcEZPjTz2sBFSsYxyj` |
| **Balance** | 0.01 BTC (unclaimed since April 2015) |
| **Contest** | KryptoKit 2014 — 30 brainwallets hidden in a promotional video |

---

## 📖 Background

In late 2014, the team behind [KryptoKit](https://kryptokit.com) and [RushWallet](https://rushwallet.com) hid **30 Bitcoin brainwallets** inside a promotional video as a contest. Passphrases were encoded in the video as visible text, subliminal flashes, repeated phrases, and other tricks.

**29 wallets have been claimed. Wallet #30 — and the passphrases for wallets #13, #23, and #26 — remain unknown.**

This repo documents everything found so far and shares the raw frames so the community can help crack what's left.

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



> ⚠️ **Must use uncompressed keys.** Compressed keys generate a different address.

---

## 🕵️ The Subliminal Text Pattern

Faint text is embedded in specific frames, only visible in the archive version. The pattern is:

```
[TEXT]  X[N]
```

`X[N]` means repeat the text `N` times to form the passphrase.

**Confirmed examples:**

| Frame region | Subliminal text | Full passphrase |
|---|---|---|
| Coins during dancing scene | `5784623964023 X2` | `5784623964023 5784623964023` |
| Dancing scene | `supercalifragilisticexpialidocious X3` | `supercalifragilisticexpialidocious` × 3 |
| Bus scene (frames 2054–2058) | `DID YOU SEE THIS X7` | *(RushWallet 2 clue — not wallet #30)* |

---

## 🗂️ This Repo

```
frames/
  found/      ← Annotated frames showing confirmed clues
video/        ← Original archive video (or see Releases if too large)
all_frames.zip
findings.md   ← Full list of all 30 wallets and what's been eliminated
```

## 🤝 How to Contribute

- **Open an issue** with a candidate passphrase and what clue it comes from
- **Submit a PR** adding findings to `findings.md`
- **Share a Wayback snapshot** of `kryptokit.com` from 2014 if you find one
- **Enhance the frames** — if you have image processing skills, try sharpening `frames/unsolved/` images

Please check `findings.md` first to avoid testing already-eliminated candidates.

---

## 📎 References

- [Wayback Machine — KryptoKit](https://web.archive.org/web/2014*/kryptokit.com)
- [Bitcoin address on blockchain explorer](https://www.blockchain.com/explorer/addresses/btc/13Q8hJqagtd77ojTJcEZPjTz2sBFSsYxyj)

---

*Investigation ongoing since 2015 · Last updated April 2026*
