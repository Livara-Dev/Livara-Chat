<p align="center">
  <a href="https://livara.org"><img src="assets/livara-logo.png" width="80" height="80" alt="Livara logo"></a>
</p>

[![Livara Chat — your conversations, your kind of space. Web and Android Beta; no phone number required.](assets/hero.svg)](https://chat.livara.org)

<p align="center">
  <b>English</b> · <a href="README.fa.md">فارسی</a>
</p>

# Livara Chat — Private Messenger for Web & Android

Your everyday conversations deserve a space that feels like yours. **Livara Chat** brings messaging, private groups, calls and shared plans together, with **no phone number required** to sign up. Start in your browser or take the Android Beta with you. [Meet Livara →](https://livara.org)

<p align="center">
  <a href="https://chat.livara.org"><b>Open Livara Chat</b></a>&nbsp;&nbsp; · &nbsp;&nbsp;
  <a href="https://livara.org/download"><b>Download Android Beta</b></a>&nbsp;&nbsp; · &nbsp;&nbsp;
  <a href="https://www.youtube.com/@Livara_Dev">Watch on YouTube</a>
</p>

---

## A little more room for connection

![Say it: messages and voice notes. Share it: calls and shared screens. Make it happen: plans and Boards. Abstract feature illustrations.](assets/features.svg)

| For your everyday | What you can do |
| :--- | :--- |
| **Keep the conversation going** | Send messages, voice notes and files; reply, react and edit. |
| **Bring your people together** | Use direct chats, private groups, voice and video calls, and screen sharing. |
| **Turn a conversation into a plan** | Organize shared work with Boards, cards and checklists. |
| **Make the space your own** | Choose themes, accents, wallpapers and typography. |
| **Get help when you want it** | Explore optional AI tools. AI API features require Livara AI Pro; review the processing settings before sharing chat context. |

[Explore the features](https://livara.org/features) · [Optional AI and plan information](https://livara.org)

## Encryption architecture · LVR1 + LGS1

<p align="center"><b>Hybrid post-quantum sessions. End-to-end encrypted conversations.</b><br><sub>ML-KEM-768 · P-256 · AES-256-GCM</sub></p>

![LVR1 hybrid sessions distribute LGS1 sender keys; devices encrypt and decrypt while the relay handles ciphertext and routing metadata.](assets/encryption.svg)

Based on Livara’s [published security architecture](https://livara.org/security), LVR1 protects direct conversations with **hybrid post-quantum end-to-end encryption (PQ E2EE)**. LGS1 protects compatible private groups with signed sender chains whose keys are distributed through pairwise LVR1 sessions.

### LVR1 · A hybrid session for two devices

LVR1 combines classical and post-quantum key material. Its post-quantum component is designed to resist future quantum decryption of recorded traffic; message encryption itself uses AES-256-GCM.

| Layer | Published design |
| :--- | :--- |
| Classical agreement | P-256 ECDH with signed prekeys |
| Post-quantum agreement | ML-KEM-768, with periodically refreshed epochs |
| Session establishment | Hybrid X3DH-style establishment; one-time keys when available |
| Key evolution | Classical double ratchet, independent sending/receiving chains, and a separate ML-KEM epoch root |
| Message protection | A message key combined with the current PQ root; AES-256-GCM protects content and header |
| Attachments | A random key for each file, delivered inside the encrypted session |

**From identity to ciphertext:**

1. **Create identity locally.** The device generates its P-256 private key and ML-KEM-768 seed. Neither is uploaded in plaintext.
2. **Check prekeys.** The client verifies signed P-256 and ML-KEM prekeys and uses one-time keys when available.
3. **Establish the session.** Several P-256 agreements and ML-KEM shared secrets establish independent classical and post-quantum roots.
4. **Evolve the keys.** One-way sending and receiving chains advance with messages. Periodic ML-KEM updates refresh the PQ root without repeating the full establishment on every send.
5. **Seal and deliver.** AES-256-GCM encrypts and authenticates the protected payload. The relay routes ciphertext; the recipient’s device opens it with the corresponding keys.

### LGS1 · Signed sender chains for private groups

Each sender maintains a separate chain instead of encrypting every ordinary group message independently for every recipient.

| Stage | What happens |
| :--- | :--- |
| Create | Each member generates a sender chain and a P-256 signing identity on their device |
| Distribute | Sender keys reach the other members through pairwise, post-quantum LVR1 sessions |
| Send | Each chain position derives a single-use AES-256-GCM key; the message carries the sender’s signature |
| Deliver | One encrypted message is distributed to the group |
| Rotate | Joining or leaving triggers fresh sender keys and redistribution |

**The PQ connection:** LGS1’s group-message cipher is AES-256-GCM; its sender-key distribution inherits the hybrid post-quantum protection of LVR1. The sender signatures described by the site use P-256.

Protected group content includes **text, edits, photos, video, files, voice notes, captions, filenames and attachment keys**. Removing a member does not erase content already received on their device.

<details>
<summary><b>Key ownership, recovery and identity checks</b></summary>

Private keys originate on user devices. Identity backups are encrypted before upload; restoring them requires the recovery phrase, not just the account password. A restored identity does not restore chat history or ratchet-session state. Compare your contact’s key fingerprint through another trusted channel.

</details>

<details>
<summary><b>Protection boundaries</b></summary>

New encrypted groups require all members to be ready. Older incompatible groups remain visibly outside E2EE, and missing encryption identity prevents a protected send. Public channels are public. Routing, membership, timestamps, ciphertext size and delivery metadata remain visible to the service; LSS1 is not active in ordinary message sending.

An unlocked or compromised device and recipient actions can expose plaintext. Optional server call recording switches calls to transport encryption with a visible **REC** indicator. Separate AI processing follows the client’s controls and privacy policy.

</details>

[Architecture](https://livara.org/security) · [Threat model](https://livara.org/threat-model) · [Local cryptography demonstrations](https://livara.org/proof)

## Your first hello

1. **Choose your platform.** [Open the web app](https://chat.livara.org) or get the current APK from the [Android download page](https://livara.org/download).
2. **Create an account.** Use a username and password; a phone number is not required.
3. **Keep your recovery material safe.** A password alone cannot restore your encryption keys. Follow the current setup and recovery instructions.
4. **Start a conversation.** Invite your people, pick a theme and make yourself at home.

For Android, compare the APK’s SHA-256 with the digest for the **same release** on the [download page](https://livara.org/download). A matching hash checks file integrity against that digest.

## Quick answers

### Does Livara work without a phone number?
Yes. Livara supports username-and-password registration. [Account overview](https://livara.org)

### Where can I use Livara Chat?
In a browser and through the Android Beta. See the [download page](https://livara.org/download) for current requirements and release details.

### Is this the application’s source repository?
This repository is a **product introduction and documentation showcase**. It does not contain the Livara Chat application source or grant a software license.

---

<p align="center">
  <b>Start with a hello.</b><br><br>
  <a href="https://chat.livara.org">Open Livara Chat</a> ·
  <a href="https://livara.org">Website</a> ·
  <a href="https://livara.org/security">Security</a> ·
  <a href="https://livara.org/proof">Proof Lab</a> ·
  <a href="https://www.youtube.com/@Livara_Dev">YouTube</a>
</p>

<p align="center"><sub>Brand artwork, not product screenshots. Product details are based on Livara’s public documentation; availability can change.</sub></p>
