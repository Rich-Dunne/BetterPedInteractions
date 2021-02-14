# Better Ped Interactions
## INSTALLATION
Drag and drop the contents from within the downloaded GTA V folder into where your GTA V is installed.  Enable the plugin in the RagePluginHook settings, or load it manually via the in-game console.
![How to drag and drop](https://i.imgur.com/0O7d7Iw.jpg)

## GET SUPPORT AND REPORT PROBLEMS
For the fastest support, [join my Discord](https://discord.gg/cUQaTNQ) and ask your question in the **correct category/channel**.  For slower support, [use this thread on the LSPDFR forums](https://www.lcpdfr.com/forums/topic/107730-richs-plugin-support-thread/).

## HOW TO XML
### Installing XMLs
XMLs must be installed within the `BetterPedInteractions` folder, which is inside the `plugins` folder.  By default, there are two folders provided within the `BetterPedInteractions` folder: `Custom` and `Default`.  You can create your own folder here.  Ultimately it doesn't matter where your XMLs are installed within the `BetterPedInteractions` folder.

### Naming XMLs
You can name your XMLs whatever you want; however, it might be beneficial to follow the naming convention `_______CivInteractions.xml` and `_______CopInteractions.xml` where the blank line is your custom name, callout pack, etc.

### XML Structuring
The basic XML layout is as follows without a sub category:
```xml
<Interactions menu="Civ">
  <MenuCategory>
        <CategoryName>Test Category</CategoryName>
        <EnableCategoryByDefault>true</EnableCategoryByDefault>
        <MenuItem>
            <Level>1</Level>
            <EnableItemByDefault>true</EnableItemByDefault>
            <BelongsToDialoguePath></BelongsToDialoguePath>
            <CategoryToEnableWhenSelected enableGlobally="false"></CategoryToEnableWhenSelected>
            <DialoguePathToEnableWhenSelected enableGlobally="false"></DialoguePathToEnableWhenSelected>
            <MenuPrompt>A menu item you say to the Ped</MenuPrompt>
            <AudioPrompt>Something you can say to trigger this menu item</AudioPrompt>
                <Response>Thank you, sir!</Response>
                <Response>Suck a butt, nerd!</Response>
        </MenuItem>
  </MenuCategory>
</Interactions>
```
Basic XML layout with a sub category, `<BelongsToDialoguePath>`, `<CategoryToEnableWhenSelected>`, and `<DialoguePathToEnableWhenSelected>` defined:
```xml
<Interactions menu="Cop">
  <MenuCategory>
        <CategoryName>Test Category</CategoryName>
        <EnableCategoryByDefault>true</EnableCategoryByDefault>
        <SubCategory>
            <CategoryName>One SubMenu for Testing</CategoryName>
            <EnableCategoryByDefault>true</EnableCategoryByDefault>
            <MenuItem>
                <Level>1</Level>
                <EnableItemByDefault>true</EnableItemByDefault>
                <BelongsToDialoguePath>My Custom Dialogue Path</BelongsToDialoguePath>
                <CategoryToEnableWhenSelected enableGlobally="true">Some Other Category</CategoryToEnableWhenSelected>
                <DialoguePathToEnableWhenSelected enableGlobally="false">Another Dialogue Path</DialoguePathToEnableWhenSelected>
                <MenuPrompt>A menu item you say to the Ped</MenuPrompt>
                <AudioPrompt>Something you can say to trigger this menu item</AudioPrompt>
                    <Response>Thank you, sir!</Response>
                    <Response>Suck a butt, nerd!</Response>
            </MenuItem>
        </SubCategory>
    </MenuCategory>
</Interactions>
```
*For more examples of the XML structure, look at the default XML files included with this plugin.*

1. All XML data must go inside the `<Interactions>` tags.  The `<Interactions>` tag has one **required** attribute, `menu`, which takes a value of *Civ* or *Cop* (values **must** be capitalized).
2. `<MenuCategory>` is the "parent" scroller menu item in the menu.  Think of this as a container for all the menu items you want to use for this category.  You can have as many `<MenuCategory>` sections as you want.
3. `<SubCategory>` is the "child" scroller menu item in the menu.  Sub categories are optional, but can allow you to better organize your dialogue options.
3. `<CategoryName>` is the name of the category or subcategory, which is the text that will appear for the scroller menu item in game.
4. `<EnableCategoryByDefault>` determines whether the category will be visible in the menu by default.  This value can be *true* or *false*.  You may want to set this to *false* if you only want it to appear after choosing certain dialogue options (explained later).
5. `<MenuItem>` is the selectable menu items in-game.  You can have as many `<MenuItem>` sections as you want.
6. `<Level>` is the "read level" required to make the menu item visible in the menu.  Each `<MenuCategory>` and `<SubCategory>` starts at level 1 and displays all enabled `<MenuItem>` elements with the same or lesser level.  In game, when a `<MenuItem>` with the same level as the category is selected, the category's level is increased by 1.  This level system allows you to hide menu items which will only be shown after selecting a certain number of menu items.  If this feature is too confusing for you, don't worry about it.
7. `<EnableItemByDefault>` determines whether the menu item will be visible in the menu by default.  This value can be *true* or *false*.  You may want to set this to *false* if you only want it to appear after choosing certain dialogue options (explained later).
8. `<BelongsToDialoguePath>` assigns the menu item to a user-defined "dialogue path."  The dialogue path system is another way of hiding and displaying specific menu items.
9. `<CategoryToEnableWhenSelected>` determines which `<MenuCategory>` or `<SubCategory>` sections to enable after the menu item is selected.  The value provided here must match a `<CategoryName>` exactly.  The `<CategoryToEnableWhenSelected>` has one **optional** attribute, `enableGlobally`, which takes a value of *true* or *false*.  If set to true, the category given in the `<CategoryToEnableWhenSelected>` tag will be enabled for **all** peds collected by the plugin.  *Note that even if a category is enabled, it will not appear if it does not have any enabled menu items.*
10. `<DialoguePathToEnableWhenSelected>` tag determines which dialogue path to enable after the menu item is selected.  The value provided here must match a `<BelongsToDialoguePath>` exactly.  The `<DialoguePathToEnableWhenSelected>` has one **optional** attribute, `enableGlobally`, which takes a value of *true* or *false*.  If set to true, the dialogue path given in the `<DialoguePathToEnableWhenSelected>` tag will be enabled for **all** peds collected by the plugin.
11. `<MenuPrompt>` is the name of the menu item, which is the text that will appear for the menu item in-game.  This also doubles as an `AudioPrompt`, which means if you're using your microphone, you can say this to trigger the menu item.
12. `<AudioPrompt>` is an alternate dialogue option you can say with your microphone (won't appear in the menu) to trigger this menu item.  You can have as many `<AudioPrompt>` items as you want.
13. `<Response>` is the response a ped can give you after you select this menu item in-game.  The `<Response>` tag has one **optional** attribute, `honesty`, which takes a value of *truth* or *lie*.  A ped's initial response is chosen at random, then will generally adhere to the ped's honesty if the attribute was defined for the chosen response.  You can have as many `<Response>` items as you want.
