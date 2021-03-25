# Better Ped Interactions
## INSTALLATION
Drag and drop the contents from within the downloaded GTA V folder into where your GTA V is installed.  Enable the plugin in the RagePluginHook settings, or load it manually via the in-game console.
![How to drag and drop](https://i.imgur.com/0O7d7Iw.jpg)

## GET SUPPORT AND REPORT PROBLEMS
Since this plugin is currently only available for Patrons, please use the appropriate channels in [the Discord server](https://discord.gg/cUQaTNQ) to report bugs and get support.

## HOW TO XML
### Installing XMLs
XMLs must be installed within the `BetterPedInteractions` folder, which is inside the `plugins` folder.  By default, there are two folders provided within the `BetterPedInteractions` folder: `Custom` and `Default`.  I use the `Default` folder for XMLs that come included with the plugin; the `Custom` folder is for your custom XMLs.  Realistically, it doesn't matter which folder the XMLs go in.

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
            <DialoguePath></DialoguePath>
            <CategoryToEnableWhenSelected enableGlobally="false"></CategoryToEnableWhenSelected>
            <DialoguePathToEnableWhenSelected enableGlobally="false"></DialoguePathToEnableWhenSelected>
            <PromptType></PromptType>
            <MenuText>A menu item you say to the Ped</MenuText>
            <AudioPrompt>Something you can say to trigger this menu item</AudioPrompt>
                <Response>Thank you, sir!</Response>
                <Response dialoguePathToEnable="some dialogue path" enableDialoguePathGlobally="false">Suck a butt, nerd!</Response>
        </MenuItem>
  </MenuCategory>
</Interactions>
```
Basic XML layout with a sub category, `<DialoguePath>`, `<CategoryToEnableWhenSelected>`, and `<DialoguePathToEnableWhenSelected>` defined:
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
                <DialoguePath>My Custom Dialogue Path</DialoguePath>
                <CategoryToEnableWhenSelected enableGlobally="true">Some Other Category</CategoryToEnableWhenSelected>
                <DialoguePathToEnableWhenSelected enableGlobally="false">Another Dialogue Path</DialoguePathToEnableWhenSelected>
                <PromptType></PromptType>
                <MenuText>A menu item you say to the Ped</MenuText>
                <AudioPrompt>Something you can say to trigger this menu item</AudioPrompt>
                    <Response>Thank you, sir!</Response>
                    <Response>Suck a butt, nerd!</Response>
            </MenuItem>
        </SubCategory>
    </MenuCategory>
</Interactions>
```
*For more examples of the XML structure, look at the default XML files included with this plugin.*

1. All XML data must go inside the `<Interactions>` elements.  The `<Interactions>` element has one **required** attribute, `menu`, which takes a value of *Civ* or *Cop* (values **must** be capitalized).
2. `<MenuCategory>` is the "parent" scroller menu item in the menu.  Think of this as a container for all the menu items you want to use for this category.  You can have as many `<MenuCategory>` sections as you want.
3. `<SubCategory>` is the "child" scroller menu item in the menu.  Sub categories are optional, but can allow you to better organize your dialogue options.
4. `<CategoryName>` is the name of the category or subcategory, which is the text that will appear for the scroller menu item in game.
5. `<EnableCategoryByDefault>` determines whether the category will be visible in the menu by default.  This value can be *true* or *false*.  You may want to set this to *false* if you only want it to appear after choosing certain dialogue options (explained later).
6. `<Action>` (not shown in above examples) is an element used to define actions which peds can be made to do.  You cannot make your own custom actions (yet?), and you probably shouldn't mess around with actions too much aside from changing their `<MenuItem>`'s `<MenuText>` and `<AudioPrompt>` values.  `<Action>` accepts the following values (must be typed exactly): *Follow*, *Dismiss*, *RollWindowDown*, *TurnOffEngine*, and *ExitVehicle*.
7. `<MenuItem>` is the selectable menu items in-game.  You can have as many `<MenuItem>` sections as you want.
8. `<Level>` is the "read level" required to make the menu item visible in the menu.  Each `<MenuCategory>` and `<SubCategory>` starts at level 1 and displays all enabled `<MenuItem>` elements with the same or lesser level.  In game, when a `<MenuItem>` with the same level as the category is selected, the category's level is increased by 1.  This level system allows you to hide menu items which will only be shown after selecting a certain number of menu items.  If this feature is too confusing for you, don't worry about it.
9. `<EnableItemByDefault>` determines whether the menu item will be visible in the menu by default.  This value can be *true* or *false*.  You may want to set this to *false* if you only want it to appear after choosing certain dialogue options (explained later).
10. `<DialoguePath>` assigns the menu item to a user-defined "dialogue path."  The dialogue path system is another way of hiding and displaying specific menu items.
11. `<CategoryToEnableWhenSelected>` determines which `<MenuCategory>` or `<SubCategory>` sections to enable after the menu item is selected.  The value provided here must match a `<CategoryName>` exactly.  The `<CategoryToEnableWhenSelected>` has one **optional** attribute, `enableGlobally`, which takes a value of *true* or *false*.  If set to true, the category given in the `<CategoryToEnableWhenSelected>` element will be enabled for **all** peds collected by the plugin.  *Note that even if a category is enabled, it will not appear if it does not have any enabled menu items.*
12. `<DialoguePathToEnableWhenSelected>` element determines which dialogue path to enable after the menu item is selected.  The value provided here must match a `<DialoguePath>` exactly.  The `<DialoguePathToEnableWhenSelected>` has one **optional** attribute, `enableGlobally`, which takes a value of *true* or *false*.  If set to true, the dialogue path given in the `<DialoguePathToEnableWhenSelected>` element will be enabled for **all** peds collected by the plugin.
14. `<PromptType>` is an optional element that defines the type of prompt the menu item is.  Currently,`<PromptType>` takes a value of *interview* or *interrogation*.  If the Agitation setting is enabled, this attribute will positively or negatively affect a ped's agitation level.
15. `<MenuText>` is the text that will appear for the menu item in-game.  This also doubles as an `AudioPrompt`, which means if you're using your microphone, you can say this to trigger the menu item.
16. `<AudioPrompt>` is an alternate dialogue option you can say with your microphone (won't appear in the menu) to trigger this menu item.  You can have as many `<AudioPrompt>` items as you want.
17. `<Response>` is the response a ped can give you after you select this menu item in-game.  The `<Response>` element has three **optional** attributes: `honesty`, `dialoguePathToEnable`, and `enableDialoguePathGlobally`.  `honesty` takes a value of *truth* or *lie*, `dialoguePathToEnable` takes a value of any dialogue path you've defined, and `enableDialoguePathGlobally` takes a value of *true* or *false*.  A ped's initial response is chosen at random, then will generally adhere to the ped's honesty if the attribute was defined for the chosen response.  You can have as many `<Response>` items as you want.
