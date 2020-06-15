---
filename: faq
---

<!--
This is an FAQ, but trailing punctuation in headings break GitHub's Markdown
convention, so if I want zero errors being flagged by VS Code, it has to look
weird. Thanks, GitHub. I'm keeping the question marks; either it gets flagged
because of trailing punctuation, or it gets flagged for inline HTML. Or both.
-->

# MOM-2236's FAQ

If I've linked you this, it's because I already have a detailed explanation to a question you asked. Its not that I am *mad*, it's just that I don't feel like typing out the same answer for the hundredth time.

## What do you do, what are these pages for?

I suppose you could call me a dataminer, but I'm interested in making mods, mainly restoring cut content in some form. Titanfall has been long since datamined, but sometimes the demo recordings of the cut content were particularly poor quality, and of course, a lot of that info is getting to be half a decade old and basically lost to time by now, with YouTube videos, Reddit posts and even a whole forum (being Facepunch in question) having been lost or deleted.

## <a name="Tools"></a>Where do I get started? What kind of tools do I use?

1. Cra0kalo's VPK tool. Version [3.4](https://github.com/mom-2236/titanfall_research/raw/master/storage/cra0kalo/Titanfall_VPKTool3.4_Portable.zip), Version [3.3](https://github.com/mom-2236/titanfall_research/raw/master/storage/cra0kalo/Titanfall_VPKTool3.3_Portable.zip), [Cra0's website](http://dev.cra0kalo.com/). Download Version 3.4 if you are unsure. It's not exactly finished (by my standards, and what I would like it to do, anyway), but Cra0 never released the source code, so I can't do anything about that. Don't bug them about it, either. It's their business to release their code if they want to, and I don't have a say in that. I've already had someone ask them about it.
2. Some form of text editor that's capable of handling code in a nice way. [Visual Studio Code](https://code.visualstudio.com/) is my weapon of choice, but you may be interested in the fork without Microsoft proprietary features such as Telemetry and licencing; it's an MIT licensed editor - [VS Codium](https://github.com/VSCodium/vscodium). Other popular editors include [Atom](https://atom.io/) and [Notepad++](https://notepad-plus-plus.org/). More free, less popular editors include Gedit and its MATE-GUI-based fork [Medit](http://mooedit.sourceforge.net/), albeit Medit doesn't receive updates for the Windows builds anymore. Gedit isn't as easy to get automatic plugin support compared to VS Code and Atom, but its got enough support to make it better than Windows NTs built in Notepad. If you choose to install Gedit via the Microsoft Windows store, it won't be free, either, unlike the other editors I have listed - you can still get the FOSS version if you download through Softonic though - Gedit itself is GPL and free to use.
3. A lot of extra hard drive space. Titanfall 1, when you install the "RF" (Region Free) also known as "ROW" (Rest-Of-World) version, contains the audio for every language of the game - the game is *big*. On top of the game, you'll have to add up to 30GB of extra, extracted data for the `mp_common` VPK, and repacking that VPK can either double (without compression) or slightly-less-than double (with compression) the size of the additional data on top of the base game, unless you choose not to backup the old VPKs (which take a long time to re-download if you mess up).
4. A lot of time, and/or a fast hard drive and fast processor. Packing VPKs takes time. A lot of time. It takes more time if you use compression, but the resulting VPK will be smaller.

## <a name="Language"></a>Can I change which language Titanfall 1 launches in?

If you have all the VPKs and the language `_dir` files for a given language downloaded from Origin, yes. Simply add the launch option of `-language English` to get English, for example. If you change language, you'll need to change which VPK `_dir` you're unpacking and replacing when you work with them in the VPK Tool. If you don't mod anything, you don't need to worry about that - just add the launch option in Origin for Titanfall 1 and it will launch it in the new language as long as you have the `_dir` files (there might be a region locked version of the game without some languages - I've also heard that the Japanese voices are broken in the ROW version; that might require some work to be usable).

## <a name="Update-when?"></a>When are you updating that model and texture guide?

I'm not updating it, and I didn't write the original. I'll write a replacement guide when I get to it. It's not high on my priority list right now.

## I don't care about all this, just tell me how to change my FOV?

[This link was in my index, too.](/titanfall_research/fov.html)

## Who are you, anyway?

People call me MOM. I enjoy Titanfall. I started out just wanting to increase my FOV, but after spending time with some other members of the Titanfall 1 community who also had experience with modifications to the game, I ended up working on much more than just changing my FOV - I've made new textures, done some datamining on my own, and worked on a few small mods. I just happen to be interested in how Titanfall 1 works, as well as all of its cut content, and whether or not it's possible to restore said content - or at least get it into a state that allows it to be demo'd for archive purposes. In my opinion, Titanfall 1 is not a finished game. A lot of content is cut, seemingly in what might have been a near-working state, but hardly any, if all, of it was ever finished for release (either its RTM, or as part of DLC). Unfortunately most of the content cannot be restored as is, because that requires server access. Some content that was unfinished did get released however; the Plasma Railgun is not a finished weapon, for instance. It was still in development, according to some of the files shipped with the game.

## How can I contact you?

You'll find me on Origin as `MOM-2236`, albeit if you have any *questions* for me, I would suggest you join the **TF\| Remnant Fleet [Discord](https://discord.gg/tWt4mBP)** - I check our \#modding channel frequently, and I'm always open to questions. If you'd like to message me directly on Discord, message `PhoenixLeLt#5869`.
