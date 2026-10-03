# Modding APIs and Libraries

Since most modders are now moving to Thunderstore and players are using mod managers that can manage dependencies, we do not need to worry as much about making users install multiple different libraries just to play your one mod. If you haven't put your mod there yet, then [do so](https://docs.smods.dev/Guides/Thunderstore/).

Until now, I have seen most developers ignore these libraries in favor of reinventing the wheel or (worse imo) trying to push every single feature into the one shared library (SMODS).

Well, hopefully that ends soon. I am presenting you here with a (non-comprehensive) list of modding APIs, libraries and popular mods with APIs to support them.

## Lovely

The main mod loader for Balatro. If you want to make a mod you need to depend on it. If you try to tell me about other ways to load mods in the replies I will come for you.

If your mod adds any kind of new gameplay content, I would recommend also depending on SMODS (see below), but if your mod only has quality of life or technical features you may prefer to depend only on Lovely to let users play your mod with a mostly vanilla environment. 

Either way, Lovely provides a way for mods to inject or replace code from the base game. This is less preferable to using one of the APIs below (that's why they exist) but unavoidable when making even a mod with intermediate complexity.

[Repository](https://github.com/ethangreen-dev/lovely-injector)
[Documentation](https://github.com/ethangreen-dev/lovely-injector#patches)

See also: [What is a patch?](https://github.com/nh6574/VanillaRemade/wiki#whats-a-patch)

## SMODS

SMODS (also called Steamodded) is the premier API for content. As in it's the only good updated one (disclaimer: I am part of the SMODS team). 

There's no space for me to describe the amount of features SMODS adds so I won't. Read the documentation. I also wrote plenty of that so it's the same.

[Repository](https://smods.dev)
[Documentation](https://docs.smods.dev)

See also: [Vanilla objects reimplemented in SMODS](https://github.nh6574.com/vanillaremade) and [example mods](https://github.com/Steamodded/examples/tree/master/Mods)

## Amulet

Amulet (an updated fork of Talisman) is a mod that allows the game to go beyond its number limits with some quality of life features for when the game needs to calculate a lot of effects.

Basically if you want to do exponents or higher it only makes sense to use this, or the player will likely run into `naneinf`. Amulet even provides SMODS-compatible calculation returns for higher operations.

For more advanced users, this provides a whole library of tools for manipulating big numbers.

[Repository](https://github.com/frostice48⁰2/amulet)

See also: [How to do exponents/hyperoperations](https://github.com/nh6574/VanillaRemade/wiki#how-do-i-add-exponential-multchips)

## Malverk

Texture pack manager and API. Use this for texture packs instead of replacing the files in the exe. Please.

The only exception is suit and rank textures (vanilla "collabs") since those are handled by [SMODS.DeckSkin](https://docs.smods.dev/Game%20Objects/SMODS.DeckSkin/).

[Repository](https://github.com/Eremel/Malverk/tree/main)
[Documentation](https://github.com/Eremel/Malverk/tree/main#defining-an-alttexture)

See also: [How to make a texture pack](https://github.com/nh6574/VanillaRemade/wiki#how-do-i-make-a-texture-pack)

## Spectrallib

A library that consolidates a bunch of different features and utilities from different mods by various SpectralPack devs.

Features include:
   - Gamesets
   - Card credits
   - Value manipulation
   - Forcetriggering
   - Automatic pluralization in localization 
   - ^mult and ^chips without Amulet
   - Deck redeeming
   - Usable Jokers
   - Level chips and mult modifications
   - Vouchers and Boosters anywhere
   - Ascension Power (from Entropy)
   - and more...

Basically if you ever wanted to copy Cryptid now you don't need to copy the code. (Please don't copy the old Cryptid code)

[Repository](https://github.com/SpectralPack/Spectrallib)
[Documentation](https://github.com/SpectralPack/Spectrallib/wiki)

## Basic Buttons

Provides a basic library to add extra buttons to Jokers (to make them usable, for example).

[Repository](https://github.com/wingedcatgirl/basic-buttons)
[Documentation](https://github.com/wingedcatgirl/basic-buttons#how-to-use-in-your-mod)

## Spectrum API

API that handles Spectrum hands (hands with more than 4 suits). 

[Repository](https://github.com/lord-ruby/SpectrumAPI)
[Documentation](https://github.com/lord-ruby/SpectrumAPI/wiki)

## Blindexpander

Allows more complex Blind effects.

[Repository](https://github.com/Mysthaps/blindexpander)

## Wallet

Allows adding custom currencies.

[Repository](https://github.com/ThunderEdge73/Wallet)
[Documentation](https://github.com/ThunderEdge73/Wallet#how-to-use-this-api)

## TheEncounter 

API for random events (similar to other roguelikes like Slay the Spire).

[Repository](https://github.com/SleepyG11/TheEncounterBalatro)
[Documentation](https://github.com/SleepyG11/TheEncounterBalatro/wiki)

## Challenger Deep

Adds new challenge rules to be used in [`SMODS.Challenge`](https://docs.smods.dev/Game%20Objects/SMODS.Challenge/).

[Repository](https://github.com/OOkayOak/Challenger-Deep)
[Documentation](https://github.com/OOkayOak/Challenger-Deep#rule-list)

## Potato Patch Utils

Adds an assortment of features used by the [Potato Patch event mods](https://github.com/Balatro-Potato-Patch).

Includes:
    - Localization Folder Handling
    - Card credits
    - Team and Developer Objects (and a credits page for them)
    - Info Menu popups
    - Description Bubbles

[Repository](https://github.com/Balatro-Potato-Patch/Potato-Patch-Utils)
[Documentation](https://github.com/Balatro-Potato-Patch/Potato-Patch-Utils#what-functionality-does-this-mod-add)

## Strange Library

Adds an assortment of utility functions used by [Strange Pencil](https://github.com/DigitalDetective47/strange-pencil).

[Repository](https://github.com/DigitalDetective47/strange-library)
[Documentation](https://github.com/DigitalDetective47/strange-library/wiki)

## TheFamily

Adds a new menu to the side with selectable cards, to consolidate new buttons into a more user-friendly menu.

[Repository](https://github.com/SleepyG11/TheFamilyBalatro)

## CardPronouns

Adds pronouns to cards.

[Repository](https://github.com/real-niacat/CardPronouns)
[Documentation](https://github.com/real-niacat/CardPronouns#for-developers)

## Others

These are mods that mostly add other content or have other quality of life features that a mod can extend through their API.

### CardSleeves

Adds an extra modifier to decks.

[Repository](https://github.com/larswijn/CardSleeves)
[Documentation](https://github.com/larswijn/CardSleeves/wiki)

### Partner

Adds a new (cute) card type present from the start of the run.

[Repository](https://github.com/Icecanno/Partner-API/)

### Penumbra

A music mod manager.

[Repository](https://github.com/lord-ruby/Penumbra)

### Silk Touch

Mobile-like controls and controller API.

[Repository](https://github.com/HuyTheKiller/SilkTouch)
[Documentation](https://github.com/HuyTheKiller/SilkTouch?tab=readme-ov-file#api-documentation-silktouchdragtarget)

### Handy

General quality of life mod. Allows defining some custom hotkeys for some objects.

[Repository](https://github.com/SleepyG11/HandyBalatro)
[Documentation](https://github.com/SleepyG11/HandyBalatro#for-developers)

### Overflow

Consumable stacking mod.

[Repository](https://github.com/lord-ruby/Overflow)

### JokerDisplay 

Show information under Jokers (this one is bad because I made it).

[Repository](https://github.nh6574.com/jokerdisplay)
[Documentation](https://github.nh6574.com/jokerdisplay/wiki)

### PlayLog

Shows a log of every action since the start of the run (this one is good because Dilly helped me make it).

[Repository](https://github.nh6574.com/playlog)
[Documentation](https://github.nh6574.com/playlog/wiki)
