# Using Mastodon with Drafts - Integration Guides - Drafts Community

"Using Mastodon with Drafts - Integration Guides - Drafts Community" - [forums.getdrafts.com](http://forums.getdrafts.com)

Updated `12272022-082455`

- [**Discourse**](https://forums.getdrafts.com/t/using-mastodon-with-drafts/13766)

---

agiletortoise | 2022-12-07 14:34:18 UTC | #1

![]()

[Mastodon](https://joinmastodon.org) is a popular decentralized, open-source, social network. Drafts supports integration with Mastodon instances through actions that can be used to post status updates and more.

## Share Extensions

If you use a client application (like the official [Mastodon app](https://joinmastodon.org/apps), [MetaText](https://github.com/metabolist/metatext), [Ivory](https://tapbots.social/@ivory/109433914793802708), etc.) to interact with your Mastodon account, your client application likely includes a Share extension available in the system share sheet. Any of these options can be used with Drafts' [Share action](https://directory.getdrafts.com/a/1YK), which opens the system share sheet.

- **Pros:**
   - No additional setup is needed.
- **Cons:**
   - Leaves Drafts to open your client app's extension.
   - Requires additional steps, like selecting the share extension in the share sheet, confirming and sending in the extension, etc.

## Mastodon Action Step

The [Mastodon action step](https://docs.getdrafts.com/docs/actions/steps/services#mastodon) provides an easy-to-configure step that posts to a Mastodon account.

The step has several options. At a minimum, the "Host" value must be configured to point to the domain of the Mastodon instance hosting your account (i.e. `mastodon.social` - see next section for setup details), and the template should be configured to output the text you wish to post - the default template `[[draft]]` uses the full text of the current draft.

Additional options control adding content warnings, setting visibility, and other options when posting.

- **Example Actions:**
   - [Post to Mastodon](https://directory.getdrafts.com/a/2FC): *Be sure to edit after install to set the "Host" domain of your Mastodon instance*.

## Action Step Setup

After installing the "Post to Mastodon" action above, there is a one-time setup needed to set the "Host" value for the action, so it knows which Mastodon instance it should be talking to...

![]()

- Edit the action (Long-press > Edit on iOS, Right-click > Edit on Mac)
- Open the steps, then the one "Mastodon" step.
- Enter "Host" value pointing to your Mastodon host. Use *just* the host name (not full URL) - like `mastodon.social`.

## Mastodon Scripting

[`Mastodon` script object](https://scripting.getdrafts.com/classes/Mastodon) is a convenience object that makes it easy to make OAuth-authenticated requests to any endpoint in the [Mastodon API](https://docs.joinmastodon.org/api/guidelines/). This unlocks the ability to do more customization to your posts, import data from your account, and many other features.

See the [`Mastodon` object documentation](https://scripting.getdrafts.com/classes/Mastodon) for details and example code, but below are a few example actions which are useful as-is or as starting points for your own ideas.

> **NOTE:** Each of these actions is setup with "Define Template Tag" steps at the beginning to provide configuration information. Be sure to edit them and set at least the first "mastodon-host" item to have a template that is the host name of your Mastodon instance.

- **Example Actions:**
   - [Post to Mastodon (Script)](https://directory.getdrafts.com/a/2FD): Simple posting action. Nothing fancy, but it demonstrates the use of a script to make a simple post.
   - [Post to Mastodon with Content Warning](https://directory.getdrafts.com/a/2FG): Scans the text of the current draft, and if you have started a line with `!` (exclamation point), the text of that line will be removed from the draft and used as the "Content Warning" for the post.
   - [Post Poll to Mastodon](https://directory.getdrafts.com/a/2FF): Use the first line of the draft as the text (e.g. the question) of the poll, and each additional line as an option you can vote on in the poll.

## Hosts, Credentials, and Multiple Accounts

Like most services integrated into Drafts, Drafts handles much of the authentication process through OAuth, storing account information in its [Credentials](https://docs.getdrafts.com/docs/settings/credentials) system.

Unlike other services, Mastodon is decentralized, so there is not a single central API to communicate with, and the credentials must be paired with the proper Mastodon instance hosting your account.

Each action (via action step or script) that talks to Mastodon, must be configured with a `host` value. This is specified in domain name form (i.e. `mastodon.social`, not a full URL), and must be set either in the configuration of the Mastodon action step, or when initializing the `Mastodon` script object instance.

If you have only one Mastodon account, simply configure the host value on each action you wish to use and you are ready to roll.

If you have more than one Mastodon account you wish to communicate with, each must have its own unique combination of host and credential identifiers. Although it can be any string value, we recommend using your `@username` account name as the credential identifier for easier identification.

The first time you run an action with a new host/identifier combination, you will be prompted to authenticate and be directed through the OAuth process.

---

pratik | 2022-12-07 21:40:27 UTC | #2

For the Post to Mastodon action, I'm getting a

```other
Script Error: ReferenceError: Can't find variable: Mastodon
Line number: 2, Column 17
```

I did change the value for `mastodon-host` in the Action. Is my Mastodon host not set up for this to work? It's sciences.social

---

agiletortoise | 2022-12-07 21:44:35 UTC | #3

Did you update to Drafts v35 (Release today)? This is a new feature that requires the update.

---

kirk | 2022-12-07 21:47:50 UTC | #4

Thank you so much for this! I've tested it on my own instance and was able to post with it. I think Drafts is now the only scriptable Mastodon app I've seen.

---

pratik | 2022-12-07 22:01:57 UTC | #5

🤦🏽‍♂️ Can you point me to where you store the 'dunce' hats?

---

agiletortoise | 2022-12-07 22:32:57 UTC | #6

No dunce hats here...it's all good. I probably should mention the version requirements in the article when it's so new.

---

Fractals | 2022-12-08 01:56:27 UTC | #7

Great addition - thankyou. I have the extension working on the Mac - but when I go over to my phone - I can see the extension - but it is greyed out. I try to edit and add my credentials - but in 'edit' only choice seems to be to toggle on or off 'step enabled on iOS/MacOS' - I am clearly doing something wrong. Any and all help welcome.

---

Fractals | 2022-12-08 02:00:59 UTC | #8

oh wait - it hasn’t updated to 35 - since I just auto updated all my apps, I assumed it had - but it hasn't. Will wit to see when update arrived. Carry on!

---

