# Balatro Mod Development FAQ

This FAQ covers frequently used fields, functions and pieces of code for Balatro mod development that are either not covered by the Vanilla examples in the main repository or that might not be entirely clear from the implementation.

## General Development

### How do I start making Balatro mods?

> [!NOTE]
> This is _not_ meant to be a tutorial on how to make Balatro mods but rather advice on how to set up your environment for developing mods.

#### 1. Install Lovely and SMODS

If you haven't already, install [Lovely](https://github.com/ethangreen-dev/lovely-injector) and [smods](https://github.com/Steamodded/smods) by following the [instructions here](https://github.com/Steamodded/smods/wiki).

It is recommended to have both updated at all times while developing as they release new features and bugfixes all the time.

You will know they're installed properly once you see the "Mods" button on the main menu and the SMODS version in the corner.

![Main Menu Screenshot](assets/Q1MainMenu.png)

#### 2. Install a code editor

You can use whatever editor you're most comfortable with, but if you're a beginner I highly _highly_ recommend using [VSCode](https://vscodium.com/). The rest of this section will have tips for VSCode but those should still apply to a lot of different editors. Please don't use notepad.

> [!NOTE]
> You don't need to be able to run a Lua interpreter manually for Balatro modding. All testing will be done through the game.

#### 3. Set up the Lua LSP

The Language Server Protocol, or LSP for short, enables features such as code completion, syntax highlighting and error markers.

[Follow the instructions here](https://luals.github.io/#install) to install it in your preferred editor. For VSCode in particular, search for "Lua" and install the [Lua extension by sumneko](https://marketplace.visualstudio.com/items?itemName=sumneko.lua).

![Extensions tab](assets/Q1Extensions.jpg)

After that, we need to point the editor to the Balatro and SMODS code so we get better completions and less undefined warnings.

To accomplish this in VSCode you can either:

- Open a folder that contains your mod, the `smods` folder and the `lovely/dump` folder (such as opening your entire Mods folder). This is the easiest way but it can lead to your workspace being disorganized and harder to navigate in.

- Set up your workspace settings so they point to those folders. You can do this either by creating a `.luarc.json` file in your mod's folder or by pressing `F1` and searching `Preferences: Open Workspace Settings` and adding the following (you can omit `Lua.` when using a luarc file):

```json
{
  "Lua.workspace.library": ["path/to/smods", "path/to/lovely/dump"]
}
```

Optionally, you can also point it to a love2d folder for more definitions or [this project by frostice482](https://github.com/frostice482/balatro-lsp) that adds more descriptions to vanilla code.

#### 4. Basic mod

Now that we have all of that we will set up a quick template mod. First, create a folder for your mod if you haven't already. (I recommend developing directly on your Balatro Mods folder for fast testing.). Open that folder in VSCode.

Create a [metadata file](https://github.com/Steamodded/smods/wiki/Mod-Metadata). For example, `coolbalatro.json`.

It should contain something similar to this.

```json
{
  "id": "MyCoolBalatroMod",
  "name": "My Cool Balatro Mod",
  "author": ["me"],
  "description": "This is my really cool balatro mod. It has XChips and Reverse Tarots.",
  "prefix": "mycoolmod",
  "main_file": "coolbalatro.lua",
  "version": "1.0.0"
}
```

> [!IMPORTANT]
> Make sure that the `id` and `prefix` are unique enough so they don't conflict with other mods. The `prefix` in particular will be used often.

Then we will set up the main file we will be developing in. File organization will be covered in a later question.

Create the file listed in `main_file`, in this case `coolbalatro.lua`. Then we will use the Joker code from VanillaRemade with some modifications to add text without a localization file using `loc_txt`.

```lua
-- Joker
SMODS.Joker {
    key = "joker",
    pos = { x = 0, y = 0 },
    rarity = 1,
    blueprint_compat = true,
    cost = 2,
    discovered = true,
    config = { extra = { mult = 4 }, },
    loc_txt = {
        name = "Joker",
        text = {
            "{C:red,s:1.1}+#1#{} Mult",
        },
    },
    loc_vars = function(self, info_queue, card)
        return { vars = { card.ability.extra.mult } }
    end,
    calculate = function(self, card, context)
        if context.joker_main then
            return {
                mult = card.ability.extra.mult
            }
        end
    end
}
```

Make sure to save often!

Now open the game and you should see your mod in the Mods menu.

![Mods Menu](assets/Q1ModsMenu.png)

![Mod Description](assets/Q1ModDescription.png)

![Added Joker](assets/Q1AddedJoker.png)

#### 5. Set up version control

When developing any software, version control is the most important aspect. This will be an extremely short guide on how to set up a git repository on GitHub using VSCode features but I highly recommend searching a tutorial on how to use git, especially if you're planning to continue to develop in the future.

First, [install git](https://git-scm.com/downloads) and create a [GitHub account](https://github.com/).

Go to your mod's folder in VSCode (For this, it can't be a folder higher up). Click on the source control tab on the side and click on "Initialize Repository".

![Initialize repository](assets/Q1InitializeRepo.png)

Then you will want to commit your work. Commiting makes it so you "save" a snapshot of how your program looks at this moment so you can go back to it at any time if anything goes wrong. It's important to commit each time you finish a task, no matter how small, and to add a meaningful commit message.

Add a message and press "Commit".

![Commiting](assets/Q1Commit.png)

Now press on "Publish Branch".

![Publish Branch](assets/Q1PublishBranch.png)

It will ask you to login to GitHub. After you do you will see this menu. You can pick between creating a Public or Private repository. This can be changed later.

![Publish Menu](assets/Q1PublishMenu.png)

Now if you go to your GitHub profile your repository should be there. Hooray!

![Repository](assets/Q1Repository.png)

> [!TIP]
> I recommend setting up a `README.md` file with information on your mod (Images are appreciated!) and a `.gitignore` file which can be used to exclude files from your repository, such as the `.luarc.json` file, the `.lovelyignore` file generated by SMODS when disabling the mod or any other reference files.

#### 6. Next steps

That's it, now you're free to go and make your Balatro dreams come true. If you have no idea what to do next, here are a couple of things to look into:

- [SMODS' Your First Mod](https://github.com/Steamodded/smods/wiki/Your-First-Mod) - Collection of resources for developing your first mod.
- [Programming in Lua](https://www.lua.org/pil/contents.html) - Recommended in the previous link but worth restating. You will need at least some basic Lua knowledge to develop mods.
- [SMODS Documentation](https://github.com/Steamodded/smods/wiki/API-Documentation) - Crucial resource when developing mods. Always have this on hand.
- [VanillaRemade](https://github.com/nh6574/VanillaRemade) - You're here right now, hi! The main repository contains all vanilla objects recreated using SMODS to use as a reference. If you can think of a similar effect in the main game, just reference the relevant code.
- [Lovely Documentation](https://github.com/ethangreen-dev/lovely-injector?tab=readme-ov-file#patches) - Documentation on Lovely patches.
- Other mods - If you know of a similar effect in another mod, most devs won't have a problem with you taking inspiration from their code. Try to be polite and ask for permission first though!
- [Balatro Discord Server](https://discord.com/invite/balatro) - The #modding-dev channel is very helpful and friendly when it comes to helping with mod development, come and ask questions! You might even see me there! Don't say hi though, I'm very timid (laughs).
- [Balatro Modding Starter Pack](https://discord.com/channels/1116389027176787968/1349064230825103441) - This specific thread in the official Balatro server contains a lot of resources to further help with development.
- Balatro's source code - If you need to recreate something that's not in VanillaRemade (or you want to specifically see the original workings), you should look at the game's source code directly. You can either access it from the `lovely/dump` folder from earlier, which contains any lovely patches done by SMODS or other mods, or by unzipping the Balatro.exe (or equivalent distribution file). Please don't redistribute the code anywhere or bother LocalThunk with any findings in the code.

### Do I need to know Lua to mod the game?

Yes, at least at a basic level.

While for the most part the code will be pretty simple, thanks to the SMODS API abstraction, if you don't have some understanding about what a for loop is or how to index a table then you might struggle. I recommend reading the recommendations above and looking up some YouTube tutorials. Keep in mind Balatro uses [`LuaJIT`](https://luajit.org/luajit.html) which in turn uses [`Lua 5.1`](https://www.lua.org/manual/5.1/) syntax, so newer features might not work.

If you really don't want to learn, try [Joker Forge](https://jokerforge.jaydchw.com/).

### Where can I find \[X\] in the game's source code?

Work in progress.

### What's a patch?

Work in progress.

### What's a hook?

Work in progress.

### How do I debug my code?

Work in progress.

### How do I organize my files?

Work in progress.

## Terminology

### What's a `front`/`center`/`back`?

Work in progress.

### What's a `pool`/`set`?

Work in progress.

### What are the different card areas called?

Work in progress.

### What's a class/mod prefix?

Work in progress.

### What's a context?

Work in progress.

### What are optional features?

Work in progress.

### What are quantum enhancements?

Work in progress.

## Making new additions

### How do I make custom art for my cards?

Work in progress.

### How can I make my card not appear in the shop/boosters/others?

Work in progress.

## Variables

### How do I check if a playing card has a specific suit/rank?

Work in progress.

### How do I get if a card has a specific edition/enhancement/seal/sticker?

Work in progress.

### How do I get the set or key of a specific card?

Work in progress.

### How do I get if the player has a certain card?

Work in progress.

### How do I get a random number?

Work in progress.

### How do I get a random element from a list?

Work in progress.

### How can I get the localized name of \[X\]?

Work in progress.

### How do I check if the score is on fire?

Work in progress.

### How do I get the most played hand?

Work in progress.

### How do I get the planet card for a specific hand?

Work in progress.

### How do I get the type of the current Blind?

Work in progress.

### How do I get if the player is in a Blind?

Work in progress.

### How do I get if the player is in a shop?

Work in progress.

## Miscellaneous effects

### How do I give \[X\] type of card to the player?

Work in progress.

### How do I immediately win/lose a Blind?

Work in progress.

### How do I immediately win/lose the run?

Work in progress.

### How do I change the Blind's requirement in the middle of a Blind?

Work in progress.

### How do I change the amount of chips scored in the middle of a Blind?

Work in progress.

### How do I change the amount of chips and mult about to be scored by the current hand?

Work in progress.

### How do I destroy cards?

Work in progress.

### How do I copy multiple cards at once?

Work in progress.

### How do I add exponential mult/chips?

Work in progress.

### How do I end the shop?

Work in progress.

### How do I cash out immediately?

Work in progress.

### How do I play music or a sound?

Work in progress.

## UI & Visual effects

### How do I add my own custom colors to use in descriptions?

Work in progress.

### How do I change the name or description of a card dynamically?

Work in progress.

### How do I add text to the description of my card that updates in real time?

Work in progress.

### How do I animate my card?

Work in progress.

### How do I add a custom tooltip to the side of the description?

Work in progress.

### How do I add a button to my card?

Work in progress.

## General mod customization

### How do I add a custom icon?

Work in progress.

### How do I add a config page?

Work in progress.

### How do I edit the main menu?

Work in progress.

## Technical questions

### How and what can I save in an game object?

Work in progress.

### How can I save something in the player's profile?

Work in progress.

### How can I can I make my own context?

Work in progress.

### How do I get if another mod is loaded?

Work in progress.

## Troubleshooting

### Why does my card crash when I change its `config`?

Work in progress.

### Why does my card crash when I hover over it in the collection?

Work in progress.

### Why does `context.end_of_round` trigger so much?

Work in progress.

### Why does the animation play before scoring when the context I put it in occurs later?

Work in progress.

### Why do I get `attempt to compare number with table` when Talisman is installed?

Work in progress.
