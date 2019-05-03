###### Credit for this guide goes to steamport, from [Sunset Station] (https://github.com/SunsetStation/SunsetStation/blob/master/sunset/README.md). Edits done by battletrap360.

# Introduction to the "skree" Folder

## Why do we use it?

To keep up-to-date with /tg/station while trying to avoid merge conflicts as much as possible, we modularize everything. This is the same method [HippieStation](https://github.com/HippieStation/HippieStation/tree/master/hippiestation) uses. The more code in the "skree" folder, the fewer conflicts will exist in future updates.

## What does it mean to modularize something?

Something is modular when it exists independent from the rest of the code. This means that by simply adding something modular to the DME file, it will exist in-game. It is not always possible to completely modularize something, but if standards are followed correctly, then there should be few to none conflicts with /tg/station in the future.

## Please mark your changes

All modifications to non-skree files should be marked.

- Multi line changes start with `// skree start` and end with `// skree end`
- You can put a messages with a change if it isn't obvious, like this: `// skree start - reason`
  - Should generally be about the reason the change was made, what it was before, or what the change is
  - Multi-line messages should start with `// skree start` and use `/* Multi line message here */` for the message itself
- Single line changes should have `// skree` or `// skree - reason`

If you need to mirror a file, or function into a yog-specific file, please leave behind a comment stating where it went.

```
// skree start - Mirrored this function in <file> for <reason>
bunch of shitcode here
// skree end
```

Once you mirror a file, please follow the above for marking your changes, this way we know what needs to be updated when a file has been mirrored.


### tgstation.dme versus skree.dme

Do not alter the tgstation.dme file. All additions and removals should be to the skree.dme file. Do not manually add files to the dme! Check the file's box in the Dream Maker program. The Dream Maker does not always use alphabetical order, and manually adding a file can cause it to reorder. This means that down the line, many PRs will contain this reorder when it could have been avoided in the first place.

### Icons, code, and sounds

Icons are notorious for conflicts. Because of this, **ALL NEW ICONS** must go in the "skree/icons" folder. There are to be no exceptions to this rule. Sounds don't cause conflicts, but for the sake of organization they are to go in the "skree/sounds" folder. No exceptions, either. Unless absolutely necessary, code should go in the "skree/code" folder. Small changes outside of the folder should be done with hook-procs. Larger changes should simply mirror the file in the "skree/code" folder.

### Defines

Defines only work if they come before the code in which they are used. Because of this, please put all defines in the `code/__DEFINES/~skree_defines' path. Use an existing file, or create a new one if necessary.

If a small addition needs to be made outside of the "skree" folder, then it should be done by adding a proc. This proc will be defined inside of the "skree" folder. By doing this, a large number of things can be done by adding just one line of code outside of the folder! If a file must be changed a lot, re-create it with the changes inside of the "skree/code" folder. **Make sure to follow the file's path correctly** (i.e. code/modules/clothing/clothing.dm.) Then, remove the original file from the skree.dme and add the new one.

## Specific cases and examples

### Clothing

New clothing items should be a subtype of "/obj/item/clothing/CLOTHINGTYPE/skree" inside of the respective clothing file. For example, replace CLOTHINGTYPE with ears to get "/obj/item/clothing/ears/skree" inside of "ears.dm" in "code/modules/clothing." If the file does not exist, create it and follow this format.

### Actions and spells

New actions and spells should use the "skree/icons/mob/actions.dmi" file. If it is a spell, put the code for the spell in "skree/code/modules/spells." To make sure that the spell uses the skree icon, please add "action_icon = 'skree/icons/mob/actions.dmi'" and the "action_icon_state" var.

### Reagents

New reagents should go inside "skree/code/modules/reagents/drug_reagents.dm." In this case, "drug_reagents" is an example, so please use or create a "toxins.dm" if you are adding a new toxin. Recipes should go inside "skree/code/modules/reagents/recipes/drug_reagents.dm." Once again, "drug_reagents" has been used as an example.

---

### Thank you for following these rules! Please contact a maintainer if you have any questions about modular code or the "skree" folder.