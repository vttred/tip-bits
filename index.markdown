---
layout: default
---

### What is Tip Bits?

Tip Bits is a Foundry VTT module that allows FVTT users to tip all authors whose modules they use. It's enabled by the Web Monetization API.

### What is the Web Monetization API?

See <https://webmonetization.org>.

### What is the Web Monetization API (the short version)?

A user pays a subscription fee to a **payment provider.** The payment provider pays part of that revenue to all WM-enabled websites the user visits. It apportions payments based on how much time the user spends on each enabled website. Websites collect payments through supported ***digital wallet providers.**

### Who are the payment providers? What are their current services?

There is currently only one payment provider, [Coil][1]. Coil only has one subscription plan: 5USD per month payable via credit card. Subscribers get a few extras from Coil's [promotional partners][2], including [Imgur][3] and [Twitch][4].

Coil also provides a free blog platform. It allows authors to lock their articles behind a WM-enabled paywall.

### Why Web Monetization? Why Coil?

Users choose a Coil subscription because they want to support creators, but don't want to open checkout workflow for a one-dollar donation. Creators choose to enable Web Monetization because it's easy (one line of HTML). Many CMS solutions already support it.

I'd be remiss not to acknowledge that Coil isn't popular. Very few Foundry users will subscribe without us advertising Coil's service. I will keep an eye out for more monetization opportunities that have better adoption potential than Coil.

### How does Coil pay creators (in general)?

After a user makes a Coil account and purchases their subscription, they will need to install the Coil browser add-on. There's also a mobile browser called [Puma][5] that natively supports Coil payments.

The extension will check each website for the monetization `<meta>` tag. Then it will check if the payment pointer is valid. If both are true, it will begin sending one micropayment every second.

Coil sends 0.36USD per hour in a cryptocurrency called XRP or Ripple. It pauses payments when the browser tab loses focus. It reduces its micropayment amount when the user has sent over 4.50USD in a single billing cycle (one month). The exact reduced rate is not documented. It will continue paying at a reduced rate until the month ends, even after reaching 5.00USD. The user isn't charged a fee for exceeding 5.00USD.

### Which of the above features are part of the Web Monetization spec, and which aren't? Is it always going to be a $5/mo subscription and 36 cents/hr payout?

See <https://webmonetization.org/specification.html>.

The payment provider client-to-digital wallet handshake is part of the spec. Payments pausing when the browser tab loses focus is also part of the spec.

The amount and frequency of payments is an implementation detail at the discretion of the payment provider, and it can change at any time. A new payment provider may allow the user to choose their payment amount or frequency.

### What is the monetization meta tag?

```html
<meta name="monetization" content="$wallet.example.com/alice">
```

### Can module authors each insert our own monetization meta tags to share payments?

No. This would likely cause a performance hit (overworking the browser extension). We insist that Tip Bits is the only Web Monetization enabler.

### What do I need to do to take part in monetization with Tip Bits?

You do not need a Coil subscription. Instead, you need to create an account with one of the supported digital wallet providers. Then you may create one or more payment pointers.

When you create your account, you will need to provide personally identifiable information. You won't have to share your most sensitive PII (*e.g.* a Driver's License photo and SSN) until you decide to withdraw funds.

Once you have your payment pointer, please send it to <tip-bits@vtt.red>. It is not a wallet secret key; it is more akin to a CashApp/Venmo username.

### How do you plan to determine payment splitting between all participating modules?

This is still to be determined. In the beginning, every module author will receive a roughly equal split. Pending a conversation with module authors, I'd like to find ways to adjust payment splits more equitably.

### What do you mean by "roughly equal?" How does Tip Bits work?

Let's recap. Coil pays every second. Tip Bits can only enable one payment pointer at a time without beginning to impact browser performance. 

Tip Bits does what it can with these constraints. Upon initialization, Tip Bits will create a manifest of payment pointers among the enabled modules in random order. Every minute, it will switch to the next payment pointer in the list. Averaged over time and users, each author will get equal payout.

After the alpha test period, Tip Bits will likely transition to a different system.

### Who are the supported digital wallet providers? What are their current services?

See <https://webmonetization.org/docs/ilp-wallets>.

There are two supported digital wallets, [Uphold][6] and [GateHub][7]. Here are some details not mentioned on the website.

GateHub failed to defend against a security breach in 2019. The breach affected over 1 million accounts.

According to Uphold's website, they still charge a "spread" for crypto-to-fiat exchanges. The spread will vary by currency.

There is a "standard network crypto withdrawal fee" that applies to both platforms.

### Can we also gate premium content based on whether web monetization is enabled?

Yes. I'll release some sample code and simple ideas for how to do that later this month. For now, you can poke around the web for the basic gist. I recommend implementing features that individual users can unlock. Features that you can unlock for the Foundry instance as a whole might be an anti-pattern.

### Can Foundry users defeat the Web Monetization paywall?

Seedy devs can edit modules to remove the paywall. If you licensed your module with an open source license, they are fully within their rights to do that. You can make the premium unlock code closed source to at least keep most users from doing so.

Crafty users can also defeat the paywall with console commands. I'm hoping as Tip Bits gets more sophisticated, we'll find ways to prevent this from happening.

### Where can we discuss this and collaborate?

Discussion is ongoing in the [League of Extraordinary Foundry VTT Developers Discord server][8]. I welcome your input at <tip-bits@vtt.red> as well.

[1]: <https://coil.com> "Coil homepage"
[2]: <https://coil.com/explore> "Coil partners"
[3]: <https://imgur.com> "Imgur homepage"
[4]: <https://twitch.tv> "Twitch homepage"
[5]: <https://pumabrowser.com/> "Puma browser homepage"
[6]: <https://uphold.com> "Uphold homepage"
[7]: <https://gatehub.net> "GateHub homepage"
[8]: <https://discord.gg/rNzh6U2qMG> "League of Extraordinary Foundry VTT Developers Discord server invite permalink"