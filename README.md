# Anatomy of an SSH Key

An interactive, single-page walkthrough of SSH keys and public-key authentication. It starts at trapdoor functions and ends at the post-quantum algorithms landing in OpenSSH in 2026.

It opens with an annotated `ssh -v` transcript. Every highlighted line links to the chapter that explains it, and by the end you can read the whole thing cold.

## What's inside

| # | Chapter | Hands-on labs |
|---|---------|---------------|
| 01 | Two keys, two jobs: symmetric vs. asymmetric, encryption vs. signatures | |
| 02 | Trapdoors: RSA and factoring | Factoring race with live chart · toy RSA key generation and signing |
| 03 | Curves: elliptic curves, ECDSA vs. Ed25519, the nonce problem | Point addition on a real curve · discrete-log brute force over a finite field |
| 04 | Agreeing on a secret: Diffie–Hellman, X25519, ML-KEM, forward secrecy | DH with paint · DH mod p |
| 05 | The handshake: RFC 4253/4252 step by step | Stepper showing what each side and an eavesdropper knows, plus a man-in-the-middle mode |
| 06 | Inside the files: `.pub` format, fingerprints, randomart, `openssh-key-v1`, `authorized_keys` options, ssh-agent | Public key decoder with byte map, SHA-256 fingerprint and randomart |
| 07 | Field guide: every OpenSSH key type, KEX and cipher, with status, sizes, speed and history | Size and speed charts · security-strength ladder · timeline |
| 08 | The quantum problem: Shor, Grover, store-now-decrypt-later, hybrids | Mosca's inequality calculator |
| 09 | What to actually run: recommendations, `sshd_config` hardening, key audits | Key picker that outputs the exact `ssh-keygen` command |
| 10 | Check yourself | 15-question quiz with explanations |

## Running it

There's no build step and there are no dependencies. The only external request is Google Fonts, and the page falls back to system fonts without it.

```sh
git clone <this repo> && cd <this repo>
python3 -m http.server 8000    # then open http://localhost:8000
```

Opening `index.html` directly in a browser also works. To host it, use GitHub Pages: **Settings → Pages → Deploy from a branch → `main` / root**.

## Accuracy notes

- Current as of **OpenSSH 10.5** (August 2026). Version numbers, defaults and removals come from the OpenSSH release notes.
- The sample keys were generated for this page. Only the public halves are embedded; the private halves were discarded. They grant access to nothing.
- The fingerprint and randomart code (the "drunken bishop") was checked byte for byte against `ssh-keygen -lv` output for the sample keys.
- The speed chart numbers come from `openssl speed` (OpenSSL 3.0.13, single thread, 2.1 GHz Xeon cloud VM). The shape of the chart is meaningful; the absolute numbers belong to that one machine.
- Hostnames and addresses are placeholders. IPs use the RFC 5737 documentation range.

## Sources

- [OpenSSH release notes](https://www.openssh.com/releasenotes.html) and [OpenSSH: Post-Quantum Cryptography](https://www.openssh.com/pq.html)
- [RFC 10042](https://www.rfc-editor.org/rfc/rfc10042): ML-KEM hybrid key exchange for SSH
- [draft-miller-sshm-composite-sigs](https://datatracker.ietf.org/doc/html/draft-miller-sshm-composite-sigs-01): ML-DSA composite signatures for SSH
- [RFC 4253](https://www.rfc-editor.org/rfc/rfc4253) and [RFC 4252](https://www.rfc-editor.org/rfc/rfc4252)
- [NIST SP 800-57 Part 1 Rev. 5](https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final), [NIST IR 8547 (draft)](https://nvlpubs.nist.gov/nistpubs/ir/2024/NIST.IR.8547.ipd.pdf), [FIPS 203](https://csrc.nist.gov/pubs/fips/203/final), [FIPS 204](https://csrc.nist.gov/pubs/fips/204/final), [FIPS 205](https://csrc.nist.gov/pubs/fips/205/final)
- [CVE-2024-31497](https://nvd.nist.gov/vuln/detail/cve-2024-31497): PuTTY P-521 nonce bias

Corrections are welcome as issues or PRs.

## License

[MIT](LICENSE)
