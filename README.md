# DELTARUNE but it's in Wingdings
## By 大佬233（DaLao233; she/her)

This mod replaces the main in-game English fonts in DELTARUNE with the Wingdings font from UNDERTALE. I was inspired by [CloudBax](https://www.youtube.com/watch?v=I8f6K7yuqIE) trying to learn to read Wingdings like a maniac and was surprised to see this wasn't a thing yet!

Thank you to the [DELTAModders Discord](https://discord.gg/3f2SR39D3M) for guiding me on how DELTARUNE fans like their mods released. 

There are no secrets or anything here, just Wingdings. If someone wants to use this for something bigger, be my guest though. 

This was built with Deltarune v1.05, the latest build (as of 26th Feb 2026) that had a few tiny fixes in it relating to the Chapter Select. 

# Installation
This mod uses xdelta patches.
- Go to `C:\Program Files (x86)\Steam\steamapps\common\DELTARUNE` (or wherever you installed DELTARUNE) and back up everything in there. Alternatively, back it up in Steam's interface. Do this to ensure your modding spree is reversible.
- Download xdelta from RHDN [here](https://www.romhacking.net/utilities/704/)
- Unzip and open the application.
- Select the folder by "Original file" and choose the ORIGINAL `data.win` for the chapter you're using. You will find this in `C:\Program Files (x86)\Steam\steamapps\common\DELTARUNE` by default (if you're on Windows). 
- Next, select the folder next to "XDelta patch" and select the patch you so graciously downloaded.
- Apply the patch!
- Repeat for each Chapter and the Chapter Select screen (that's the one outside the chapter folders) for maximum Gasteriness *vomits* ...I can't believe I just said that.

# Issues
I probably won't fix these as I am typically quite busy and this was basically a night of ADHD hyperfixations made manifest.
- The font is a bit large for certain scenarios (e.g. The Legend cutscene) but it's cursed so I'm keeping it. 
- Text like "RECRUIT" and "SPARE" use sprites which means I would have to actually draw things if I wanted to turn it into Wingdings. I haven't an artistic bone in my body, so I haven't done that.
- Tenna's `funnytext` isn't changed for the same reason as above. I am not an artist. If someone WANTS to do it then go crazy it'd be awesome lol

Regarding the size, I - In Japanese I am 90% sure the game will either crash or not render text properly. I generally didn't touch it but there's some bits of code that may mess up sometimes. There is probably a broader thing for this. Gaster's text in UNDERTALE is kind of crazy so it may just be...a feature? You're probably here to mess around rather than actually read the Wingdings so...meh. 

Also hi if you read this far you're AWESOME thank you for being interested in this!

# How this works
My method works for any font replacement, but is quite scuffed and could be done better (e.g. By using a find/replace - I did this manually because I am too stupid to find whatever find/replace exists in the Undertale Mod Tool). 
- Take the UNDERTALE Wingdings font and extract it with [UnderaleModTool](https://github.com/UnderminersTeam/UndertaleModTool) using Scripts -> Resource Exporter -> `ExportAllFonts.csx`. 
- Go to the folder you extracted it all to and then delete everything except Wingdings. 
- Open a DELTARUNE `data.win` and go to Scripts -> Resource Importers -> `ImportFonts.csx`. This will add the Undertale Wingdings to the game, but it won't do anything until you actually set it up. The default script also does not allow individual importing, only an entire one, so just keep the wingdings files in their own singular folder.
- Use Find -> Search in Code to search for `scr_84_set_draw_font`, `draw_set_font`, `scr_texttype`, and anything like that. Familiarise yourself with it, because it is what you are editing. 
- Go to `function scr_84_init_localization()` and scroll until you find this:
```
        else
        {
            var fm = global.font_map;
            ds_map_add(fm, "main", fnt_main);
            ds_map_add(fm, "mainbig", fnt_mainbig);
            ds_map_add(fm, "tinynoelle", fnt_tinynoelle);
            ds_map_add(fm, "dotumche", fnt_dotumche);
            ds_map_add(fm, "comicsans", fnt_comicsans);
            ds_map_add(fm, "small", fnt_small);
```
- Replace all `fnt_XXX` instances with `fnt_wingdings`. Do not touch the `"XXX"` instances, these are labels the game uses. Replacing those across the whole game takes way too long!!!!
- Next, search `draw_set_font`. These hardcode fonts whereas the above aren't. You need to manually replace all `draw_set_font(fnt_notwingdings);` with `draw_set_font(fnt_wingdings);` now. This is how the menus pick their fonts! However, do not edit anything with `ja` in it, as it's Japanese and the font we're using may not work well there (not tested but like...wingdings is for Latin script, not Kana...). Whenever you see `"these quotation marks"` in `draw_set_font(...);`, do NOT replace it, as that will point to something you replaced with Wingdings anyway.
- The game should now play in Wingdings. 

If you get an error about receiving a bad argument or something, your replacement was probably bad. Try searching the code for more stuff. 

When doing Chapter 1 I didn't realise the `ds_map_add` was so efficient (DELTARUNE's code makes me want to explode) so I replaced literally every instance of `main` and so on like a fool. 

Note that Chapter 3's `funnytext` is not edited as that means having an artistic bone in my body (horrifying) (evil) (stop get it away!!). This chapter also hardcodes fonts more than any other chapter, mainly for its `8bit` segments. 

## For the Chapter Select
Chapter Select uses `_font` with numbered variables (1 for JP, 2 for EN) for its font selection. To change this to Wingdings, import the Wingdings font as above and write `fnt_wingdings` where you see a `2`. It will autocorrect to whatever is equivalent (in my experience, `10`). It will look really cursed when you get it up. 

# Suggestions for the brainrotted fans
If you are actually serious about learning Wingdings and somehow got here, then you are probably already set. If you know how the dialogue works already, then you will be able to organically learn what glyph corresponds to what letter quite quickly. 

However, as many characters in DELTARUNE speak with regular upper/lower case, you will not see characters talking like your favourite W.D. Gaster most of the time.

If you want something supplemental, you could take an English sentences AnkiDroid flashcard deck and append a CSS font with Wingdings to learn it more I guess?

# Misc. notes
- The text uses a Wingdings font, not Wingdings Unicode; this isn't really an issue and more of a description. Changing every string into Wingdings and accomodating it would be way more trouble than it's worth and it's not how Tobyfox did it anyway.

CREDITS
- Determined_Memories - Fixing the chapter select
