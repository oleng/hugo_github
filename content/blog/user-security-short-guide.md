---
title: "User security: short guide"
date: 2020-01-01T12:02:39Z
tags: [ "security", "best-practice"]
draft: false
---

> ##### Disclaimers:
> **This is not a comprehensive list**. Complete security practice includes everything from user actions, hardwares, network, softwares, attack theories & methods, time frame period &etc, in other word _NOT_ short or simple.
> I am not a professional security, do not trust easily. AFAIK as of today these are valid, re-evaluation in the future is necessary.
> Critiques, inputs and questions are welcome.

Rule of thumbs on improving online security (authentication, more security than privacy) for common users:

1. Insecure practices from web service side:
    - require password only for authentication, no 2FA.
    - sending password in plain text over email/non-encrypted channels.
    - plain HTTP or invalid certificate for HTTPS
    - SMS OTP
    - non-removable/deletable user profile (combined with other practices)
    - storing user name & passwords in database instead of salted hashes, as well as salt reuse/recycle.
    - using weak cryptographic algorithm.
    - failed to patch system vulnerabilities.
2. Insecure user practices:
    - using same password for multiple service logins
    - using public information for password (birth day, name)
    - writing passwords into unsecured list (sticky note on desktop file/monitor/desk)
    - using dubious (especially mobile) apps
    - clicking links without examinations
    - too many others
3. Do's & don'ts:
    - **Do** use password manager with strong cryptography (encryption) default (at least sha256) to generate different password for every online services.
    - Mnemonic paraphrase/sentence like `Stranger sophisticated hobos institution taichi Master aerobic novices` is much harder to crack than `m%y$p^a*s?s#W0rD`. See related [explain xkcd wiki](https://www.explainxkcd.com/wiki/index.php/936:_Password_Strength). Longer is better.
    - **Don't** use LastPass password manager, it has been bought recently by distrusted company, LogMeIn.
    - On that note: pick open source if possible, [BitWarden](https://help.bitwarden.com/) is recommended for willingness to be externally audited (which means outsiders can expose vulnerabilities and can lead to faster fix time period), also option on self-hosting server installation.
    - **Do** understand what Multi-Factor Authentication (MFA) is [^1].
    - **Do** enable Two-Factor Authentication (2FA or U2F[^2]) for everything, including your password manager.
    - **Don't** make SMS or phone number as main 2FA factor, SMS is insecure [^3], SIM card is clone-able. They're less secure compared to 2FA Time-based One-time Password (TOTP[^4]) due to lack of time constraint & flexibility. With 2FA you're not tied to a phone number or even mobile device, attacker must regain both access and generate the code in short time. TOTP is still vulnerable to social engineering attack. Another plus is giving away phone number on the internet isn't needed anymore.
    - **Do** use 2FA application at least, U2F hardware[^5] (usually in the form of USB dongle) is preferable because of additional protection measures to harden embedded cryptoprocessor's security[^6], such as against physical tampering. U2F hardwares also don't store account details, which means if someone steals it they can't gain access to any online accounts that device had used to authenticate with, unlike 2FA apps.
    - [Authy](https://authy.com/) is better than Google Authenticator app because with the latter you're locked to a single device.
    - Make sure you find out beforehand what to do (preventing exploit & regaining access) if you lose your device that contains your 2FA app.
    - Eventually password as authentication method on the web will be replaced and made obsolete.
    - **Do** develop security best practices, assess your devices & services. Research is key.

##### Common terms

[Phishing](https://en.wikipedia.org/wiki/Phishing)
: a social engineering technique to get sensitive informations from human in order to gain access to targeted accounts.

[Man in the middle (MITM)](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)
: an attacking technique done by hijacking, intercepting,  manipulating and spoofing data in a network.

[Spoofing](https://en.wikipedia.org/wiki/Spoofing_attack)
: posing as an entity (computer, network address, human, metadata)


##### Cases

Current trend in Indonesia is e-wallet targeting phishing. Search social media for phishing OTP code for popular e-wallets, at times involving delivery drivers.
https://twitter.com/feyzheng/status/1211341794325061632?s=20

SMS based phishing & swapping SIM cards.
https://nakedsecurity.sophos.com/2018/12/21/more-phishing-attacks-on-yahoo-and-gmail-sms-2fa-authentication/ [^7]


It's worth reminding that **social engineering** is extremely popular because it's easier to deceive a human than hacking a system or network, meaning your security depends a lot more on your security awareness than threats that comes from complicated technical attack. And that the worst possible result for individuals isn't just losing some amount of money, but ones from [identity theft](https://en.wikipedia.org/wiki/Identity_theft).



[^1]: The simplified explanation of what factors usually means is each of these: something user _knows_, something user _has_, and something user _is_.  https://www.yubico.com/what-is-multi-factor-authentication/#av_section_4
[^2]: FIDO ([*F*ast *ID*entity *O*nline Alliance](https://fidoalliance.org/overview/)) is a consortium that develops authentication standards. FIDO Universal 2nd Factor (U2F) standard, client protocol that currently is widely supported, has been renamed to CTAP1 (Client-to-Authenticator version 1), while the next standard is called [CTAP2](https://fidoalliance.org/specs/fido-v2.0-ps-20190130/fido-client-to-authenticator-protocol-v2.0-ps-20190130.html). Together with W3C's [WebAuthn specification](https://www.w3.org/TR/webauthn-1/) support, they're known as FIDO2 Project.

[^3]: https://pages.nist.gov/800-63-3/sp800-63b.html#81-authenticator-threats

[^4]: https://en.wikipedia.org/wiki/Time-based_One-time_Password_algorithm#Weaknesses_and_vulnerabilities

[^5]: [Yubikey](https://www.yubico.com/why-yubico/for-individuals/#account_protec) is a trusted, most widely used key device by tech companies.

[^6]: https://en.wikipedia.org/wiki/Secure_cryptoprocessor

[^7]: https://security.stackexchange.com/questions/11493/how-hard-is-it-to-intercept-sms-two-factor-authentication/11512#11512
