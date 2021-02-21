# Macrology: A Guide to Macro in FFXIV (the Third Edition)
## Preface  
Since Macrology (the Second Edition) published, Innovative using of macros have been concerned by all Eorzea around. Many players' prejudice to macro has been eliminated, and more players gained convenience from macros.  

The Second Edition was published at patch 4.3, which has been a long time. After several patches, some details are no longer suitable. And due to some reasons, almost all images are missing, which is hard to fix. So comes the Third Edition.  

In this edition, we replace actions from 4.X with 5.X ones, record new gif for demonstration, and add new chapter about **advanced macro analysis frame by frame** and **hotbar-change Macro System logic guide diagram**, in order to help readers to understand these macros. We also reorganize the structure and add new chapters to describe more wonderful macro toys and theories.  

You may doubt it useless since macro in FFXIV is extremely weak compared to macros in other MMORPGs, but macro only useful when meticulous research and design are made. Macrology has another meaning: cumbersome sentences. Macro is so cumbersome that only by cumbersome design can we realize functions with high value and creativity. If you desire to do something great by macro, research it carefully with your creativity. **You'd better not using any macros which you don't know how it works.** Without understanding it, you cannot predict and solve the problems, finally result in party wipe at HP 0.1% probably.  

Macrology is extensive and profound, new theories and technologies emerge in endlessly. Author's ability is limited, if you find any shortcomings or mistakes, feel free to point out.  

Special thanks to all members of MacroEorzea.  

Permission is not needed to distribute this work, but please note the original page.  
Author: Suzune Tsukuyomi@Ixion, Mana.  

## Explanation
This article is theoretical. All researches do not directly serve the actual combat, nor provide the actual combat data proof.  

All rotations in this article are probably not the best rotation, just for example.

Some macros in this article are incompleted. Please complete them by yourself as a little test.  

If you want to learn some basic knowledge of text commands and macros or copy some macros that can be used directly without modification, please read Part 1. 

If you want to learn some widely used advanced macro system, please read Part 2.  

If you want to go deep into the field of Macrology, reduce macro amount or develop very complex macros, please read Part 3.  

Never reply to those who just ask for a completed macro.  

This article is translated from Chinese. Examples are changed to better fit English conditions some example is deleted due to no suitable example in English conditions.  

TL; DR: If you already know basic macros well, read "Hotbar" in Part 1 than start from "Message Macro Type ASWC" in Part 2.  

## Index
### Part 1 Basic Macro
- Introduction
- Macro Panel
- Text Command and Macro
- Characteristics of Macro
- Placeholder
- Local Processing
- Action Queue
- /ac
- /wait and <wait.X>
- Hotbar
- /hotbar
- Chatting Command
- Macro-controlling Text Command
- Examples
- Debug
- Conclusion

### Part 2 Advanced Macro
- Introduction
- FAQ
- Abbreviation
- Message Macro Type ASWC
- Action State-system
- hotbar-change Macro System
- hotbar-change Macro System Logic Guide Diagram
- Combo Macro System Type ASWC
- Exhibition Macro
- Menu Macro System
- Conclusion

### Part 3 Uncommon Macro
- Process Guiding Macro
- Priority Macro
- Rolling Macro System
- Pseudo-random Macro System
- Multistage Fallback Macro System
- Multi-purpose Macro and Shared Hotbar
- Macro at Low Frames
- Core Framework of Macro
- Tricks
- Unsolvable Problem
- Macrology Acrobatics
- Macrology Thought
- Sharing
- Postscript

# Part 1 Basic Macro
## Introduction
This part elaborates basic knowledge of macro. Skilled in macro or not, there can be something new to you.  
In this part, you can learn:  
- How to use macro panel
- Basic principle of macro
- Independence and objective existence of hotbar
- Distinguishing macros that significantly reduce your DPS
- Important text command
- Writing simple macro

## Macro Panel
Press Esc or select system in main menu, then select User Macros to open macro panel. You can also bind a hotkey to it in `Keybind`.  
![](img/panel.png)  
(This image is from CN client. Everything is at the same position on other clients so don't worry)   
1. Individual/shared macro page change. Macros in individual page can only be used by this character, while ones in shared page can be used by all characters logged in on this client. If you want to share your individual macros, you can copy and paste macro.dat in your character folder to other folders.
2. Macro icon. Click it to choose a system-provided icon. You can also use /micon to assign. If not assigned, it will get a default icon ![](img/default_icon.png) .
3. Macro name. It will display when mouse over or in cross hotbar.
4. Name letters limit. You can only name it within 20 letters.
5. Macro content. You'd better write with text command.
6. Content line limit. You can write up to 15 lines, 180 letters per line.
7. Macro list. Every slot can save a macro. You can drag it to hotbar, but can't drag to other slots. You can right-click to call out the submenu.
8. the number of macro you are targeting.
9. Used slots this page.
10. Text command list. Since it is hard to find the command you want without searching, you'd better use /? or go to https://na.finalfantasyxiv.com/lodestone/playguide/db/text_command/  

There are several submenu options:
- Execute: execute it once.
- Copy: copy it. Cannot paste it out of panel.
- Cut: cut it. If there are hotkeys of this macro on hotbar, delete them.
- Paste: paste it. Overwrite this slot if any macro exists.
- Delete: delete it. If there are hotkeys of this macro on hotbar, delete them.
- Undo: reverse delete, cut, paste or redo. You can only undo once. If there are deleted hotkeys, they won't be restored.
- Redo: undo the undo. 
- Set to Hotbar: assign a hotkey of this macro to your cross hotbar.

## Text Command and Macro
So, what is exactly macro? In FFXIV, macro is a program-like text command set which can instead players' operation. Question raises again that what is exactly text command? In game we can press the hotkey to cast an action, and by execute `/ac "action name"`, we can also cast this action. This text command instead the operation that pressing the hotkey. You can use placeholder in text command, like `<me>` instead of inputting your ID. FFXIV doesn't have a special text command inputting area, and all commands should be input in chat window with a `/` at the beginning to distinguish from chatting messages. **If this `/` missing or not at the beginning, your command will be sent as a chatting massage.** Most commands have abbreviated forms and localized forms, you can use anyone you like while we suggest using auto-translation so that you can use your macro on other clients. There are so many text commands that we can only show you ones of most importance. If you meet any command you don't know, give it a try!  

Inputting text command again and again can be tedious. We can store frequently-used commands in a program so we can run it to input and execute faster. This program is exactly macro. A macro can store up to 15 lines of commands. Running macro will input and execute stored commands line by line in a very short time (1 frame per line). **If there are any lines not start with a `/`, it will be sent as chatting massage.** Macro ends if meeting a blank line. Almost all text command can be executed in macro, and there are also some macro-controlling command.  

## Characteristics of Macro
There are two basic characteristics of macro: one direction, one lane.
- One direction means macro execute its command line by line. All lines below will wait until former line complete its execution. No condition or loop is accepted. Macro knows no result, nor executable or not. This makes macro hard to programming. **Note that "complete its execution" means command executed instead of character's action.** `/ac` cost one frame to execute. If character cannot use this action at this time, this command will also be executed, callback that "you cannot do this" and completed.   
- One lane means only one macro can be run at the same time. If you run a new macro before previous macro ends, previous one will be shut down at once. If previous one has a macro lock (`/mlock`), no macro can be run until it ends. **Note that inputting text command by yourself won't interrupt previous macro, nor prevented by macro lock.** That is because text command is different from macro, though macro is consist by text commands.  

## Placeholder
Placeholder is an element of text. Different from others, placeholder can change itself logically to meet current state. Placeholder looks like `<...>`, present a logical object. It's the only element that can change itself. When line sent, placeholder will be replaced by its logical object. For example, "`Provoke => <t>`", if target names "Fatebreaker", it will change to "`Provoke => Fatebreaker`". Players in other languages will see the name in their own languages. If logical object does not exist, placeholder will change to `None` (not blank or space).  

Placeholder can be used in text command. Except using in chatting commands, it can also become a parameter of other commands. Like `<tt>`, target's target, we call them logical targets. Due to World Traveling system launched in patch 4.5, we can no longer use ID instead of placeholder except `/tell`. Placeholder list is not available in game, for details, please read https://na.finalfantasyxiv.com/lodestone/playguide/db/text_command/placeholder/  
  
There are two placeholders not as the same as others. `<wait.X>` is a controlling command, equals to `/wait` (see below). It and anything after it will not appear in messages. `<se.X>` will ring a sound in party/alliance/echo. it won't change to other forms.  

## Local Processing
Macro and text command instead player's operation. All these will change to a same form in system. All player's operation is local, so macro and text command are also local. They will be executed at once no matter how poor your network connection is.  

You may feel disagree with this, for when network connection is poor, macro works not well. This is actually because macro is running as before, but connection with server is not as before. When you use a crafting macro, some actions missing if network connection is poor, this not because macro are influenced by network connection, but macro execute its commands as usual while character cannot receive commands due to poor network connection.  

## Action Queue
Except Draw and Mudra, all actions are handled at servers. This causes a delay, and action queue compensate it. When you press an action hotkey, if you cannot cast this action now but you can after no more than about 0.5s, this action will be queued in, and cast automatically once you can. Therefore, by pressing hotkey you can cast next action as soon as you can, increasing your uptime. Without it, only after action ready can you press it effectively, result in a little delay about 0.1s, and greatly reduction of your DPS due to less GCDs. **Note that action cast by text command cannot be queued in.**

## /ac
```
ALIASES:
　/action, /ac
USAGE:
　/action "action name" [placeholder]
→Uses an action on the specified PC. Uses current target when not specified. Target does not need to be specified for certain actions. This cannot be used with actions you have not yet learned, or when restricted by other factors. If action uses ground targeting, then the action will be executed on the specified PC. If no PC is specified, then you will enter ground targeting mode.
>>Examples:
　/action "Heavy Swing" <t>
　(Executes Heavy Swing on current target.)
　/action "Cure" <2>
　(Executes cure on second player in party list.)
```
- **Note that if you execute this command when cannot cast this action at once, this command will do nothing.** 
- Action name should be original action, e.g., Input `/ac Iaijutsu` to cast `Midare Setsugekka`, or input `/ac Veraero` to cast `Verholy`.
- If you cast a ground-targeting action, the center of circle will be set at target's center (If you cannot reach this center, it cannot be cast, pay attention when target is very big or far). 
- If you specify an upgradable action, no matter which one you specify, the highest grade you learned will be cast.
- Each command cost **1 frame**.  

Most players write their first macro with this command. It has endless charm, tempting beginners to use it. Then you write some "`one-click`" macro, and find it awful. Action cast by `/ac` cannot be queued in. Don't use `/ac` to cast GCD action if possible. **Note that not every macro reduce your DPS, only when you continuously cast GCD action by `/ac`.** We mostly not use this command alone, just use it for patch in advanced macro.  

But sometimes we can also use it. It performs well in priority. When several actions have a similar function but different efficiency, the action with higher efficiency should be cast first. Or an action procs another action, so you should cast the latter one first to avoid overwriting. For example, `Precise Touch` can completely replace `Basic Touch`. we can write a macro like this:  
```
/ac "Precise Touch"
/ac "Basic Touch"
```

There are some other examples of single /ac:
- Cast actions that must be cast out of combat. The following macro can refresh your Mudra without affecting your movement speed.
  ```
  /ac "Hide" <wait.2>
  /statusoff "Hidden"
  ```

- Cast actions by priority. You'd better only use this on ability. You may not feel well, but do not affect your combat except using at very last this phase. Due to 1 frame per line, there is little chance that the latter one will be cast first.
  ```
  /ac "Fan Dance III"
  /ac "Fan Dance"
  ```   
- Cast actions which target ground. This helps you cast them quicker, but not able to precisely targeting.
  ```
  /ac "Sacred Soil" <t>
  ```
- Cast actions without targeting. This can save your operation to change target, preventing you from missing auto-attack. You'd better not use this on GCD healing magic, though it won't affect too much.
  ```
  /ac "Nature's Minne" <tt>
  ```
- Cast crafting/gathering actions. You may have seen a lot of examples somewhere else.
  ```
  /ac Reflect <wait.3>
  /ac Innovation <wait.2>
  /ac "Preparatory Touch" <wait.3>
  /ac "Great Strides" <wait.2>
  /ac "Byregot's Blessing" <wait.3>
  /ac Veneration <wait.2>
  /ac Groundwork <wait.3>
  /echo Craft finished <se.2>
  ```
- `[Advanced]`Prevent actions from being queued in. Most used in Mudra. There's no appropriate example that can be shown.

## /wait and <wait.X>
```
USAGE:
　/wait [wait time]
→A macro command for adjusting the pause between commands. A wait time amount of 1 equals one second. The maximum wait time allowed is 60. If the wait time amount is over 60, it will be counted as 60.
```
When macro meeting a `/wait` or `<wait.X>`, it will wait specified seconds before execute next line. 
- If you specific a float number, it will be rounded. 
- `<wait.X>` equals to `/wait`, but doesn't cost a single line, which helps a lot for 15 lines limit.
- If you omit `[wait time]`, it will be judged as 1.
- In fact, this command can be used out of macros. When a `/wait` input manually, macros will wait the specified seconds after the executing line complete. If the executing line is also `/wait`, it will be skipped. 

Due to one lane, `/wait` without a macro lock is easy to be interrupted. Macro lock prevents other macros which may be of importance. Therefore, we hardly use a long `/wait` except you are sure no more macro is needed for this time.

There are some other examples of `/wait`:
- Cast repeated actions when you are extremely boring and no more DPS required.
  ```
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /ac Holy <wait.3>
  /e One more Holy macro <se.1>
  ```
- Send messages after actions.
  ```
  /ac "Hallowed Ground"
  /p I AM IMMORTAL!!! <se.1>
  /wait 10
  /p Man is mortal...<se.2>
  ```
- Prevent your messages filling the scene when pressing key repeatedly.
  ```
  /ac Shirk <2>
  /wait 1
  /p Shirk => <2> <se.3>
  ```   
- `[Advanced]`Realize condition branch by different animation lock. The following macro can cast 4 `Hasty` and 1 `Basic Touch`, while at most one of them can be replaced by `Precise Touch`.
  ```
  /ac "Precise Touch" <wait.1>
  /ac Hasty <wait.2>
  /ac Hasty <wait.1>
  /ac "Precise Touch" <wait.1>
  /ac Hasty <wait.2>
  /ac Hasty <wait.1>
  /ac "Precise Touch" <wait.1>
  /ac Hasty <wait.2>
  /ac Hasty <wait.1>
  /ac "Precise Touch" <wait.1>
  /ac Hasty <wait.2>
  /ac Hasty <wait.1>
  /ac "Precise Touch"
  /ac "Basic Touch"
  ```

## Hotbar
Hotbar is short for hotkey bar, also called as action bar. There are many kinds of hotkey that can be placed on hotbar. Each class or job has 10 special hotbars. All classes and jobs share 10 shared hotbars. The number of shared hotbar is black ![](img/share5.png), while one of the job-specific hotbar is white ![](img/X5.png). Each hotbar has 12 slots. 

There is also a crosshotbar, which mostly used by controller user, but players who use keyboard and mouse can also call it out in `HUD Layout`. Each class or job has 8 crosshotbars. Each crosshotbar has 16 slots. Crosshotbar is independent from hotbar.

In PVP area, there is also a pvphotbar and a pvpcrosshotbar. They are also independent and cannot communicate with PVE ones.

System calls these special hotbars "`[Job name(abbr.)] [number]`". Shared hotbars called "`share [number]`". A character always has 390 hotbars (9 classes, 18 jobs, 8 crafters, 3 gatherers and 1 shared), no matter anything. Even if you haven't unlocked that class/job, it still exists and you can use `/hotbar copy` to modify it. 

But you can only display at most 10 hotbars. You can only display hotbars which are special for current class/job or shared. You cannot display a special hotbar and a shared hotbar which have the same number at the same time. Default setting is displaying `special 1` and `special 2`, hiding `special 3` and `share 4-10`. You can change the visibility of hotbars via `HUD Layout`, `Character Configuration` or execute `/hotbar display X [on/off]`. You can change displaying shared hotbar or special one of this number via `Character Configuration` or execute `/hotbar share X [on/off]`. Note that shared hotbar is independent. If you execute `/hotbar share X off`, hotkey on it won't be deleted, just you can't see it. 

**It cannot be overemphasized that hotbar is independent and objective existent.** Independence means that nothing will be changed if you modify another hotbar with the same number. When you modify `NIN 4`, `ROG 4` and `share 4` are unchanged. The first hotbar can be changed to show other hotbars while using keybind of the first hotbar, but it won't change hotkeys on hotbar 1. Objective existence means that visibility do not affect the hotkey on hotbar, just you can't see it. You can also use `/hotbar copy` to set hotkeys on invisible hotbars. You can press the same hotkey to cast action on the hidden hotbar. Note that you cannot press the hotkey on undisplayable hotbar, like you can't cast your potion on the BLM's hotbar when you are SMN. 

Hotbar is extremely important in advanced macro. You will use a lot of hidden hotbars to realize your goal. You'd better hold an Excel to note down each hotbar is used for what if you want to go deeper in Macrology, or you may mistakenly overwrite hotbars which have been used by other macros, result in chaos.

## /hotbar
```
USAGE:
　/hotbar [subcommand]
→Edit and configure hotbar settings. Only available in PvE areas.
>>Subcommands
　action "action name" [#1] [#2]
　　Set the specified action to slot [#2] in hotbar page [#1]. If "current" is entered for [#1], then the action will be set in the page displayed in hotbar 1. If [#2] is omitted, the action will be set to the lowest-numbered slot available. If both [#1] and [#2] are omitted, the action will be set to the lowest-numbered slot available on the lowest-numbered hotbar available. This applies to all of the following subcommands.
　blueaction "blue mage action name" [#1] [#2]
　　Set the specified blue mage action to slot [#2] in hotbar [#1].
　general "general action name" [#1] [#2]
　　Set the specified general action to slot [#2] in hotbar [#1].
　item "item name" [#1] [#2]
　　Set the specified item to slot [#2] in hotbar [#1].
　emote "emote name" [#1] [#2]
　　Set the specified emote to slot [#2] in hotbar [#1].
　companion "companion action name" [#1] [#2]
　　Set the specified companion action to slot [#2] in hotbar [#1].
　pet "action name" [#1] [#2]
　　Set the specified pet action to slot [#2] in hotbar [#1].
　minion "minion name" [#1] [#2]
　　Set the specified minion to slot [#2] in hotbar [#1].
　mount "mount name" [#1] [#2]
　　Set the specified mount to slot [#2] in hotbar [#1].
　enemysign "enemy sign name" [#1] [#2]
　　Set the specified enemy sign to slot [#2] in hotbar [#1].
　waymark "waymark name" [#1] [#2]
　　Set the specified waymark to slot [#2] in hotbar [#1].
　change [number]
　　Replace current hotbar with hotbar [number]. If "next" or "prev" is entered in [number], then you can scroll through the pages of hotbar 1.
　copy [class 1] [#1] [class 2] [#2]
　　Copy the contents of [class 1] hotbar [#1] to the [class 2] hotbar [#2].
　　The subcommand "current" can be used to specify your current class.
　　The subcommand "share" can be used instead of a class to specify your shared hotbar.
　display [number] on
　　Display hotbar [number].
　display [number] off
　　Hide hotbar [number].
　display [number]
　　Toggle on/off hotbar [number].
　share [number] on
　　Make hotbar [number] shared.
　share [number] off
　　Unshare hotbar [number] and assign it to your current class/job.
　share [number]
　　Toggle between on/off.
　remove [#1] [#2]
　　Remove the action assigned to slot [#2] on hotbar [#1].
　　Replace [#2] with "all" to remove all actions from hotbar [#1].
>>Examples:
　/hotbar action "Mount Roulette" 1 1
　(Places Mount Roulette in slot [#1] on hotbar [#1].)
　/hotbar change 2
　(Replaces hotbar [#1] with hotbar [#2].)
```

...Extremely complex right? This is the most complex command. Use `/crosshotbar` or `/chotbar` or `/xhb` for crosshotbar, `/pvphotbar` for pvphotbar and `/pvpcrosshotbar` for pvpcrosshotbar. Everything is almost the same. Note that you cannot use `/hotbar` or `/crosshotbar` in PVP area, nor `/pvphotbar` or `/pvpcrosshotbar` in PVE area. If the subcommand has something wrong at the tail, but the former part can be a completed command, it will be executed as a completed command, ignoring the wrong part.

We will start our learning from its subcommands.

### share
USAGE `/hotbar share [hotbar number] [on/off]`  

Change displaying shared hotbar or special one of specified number. If omitting `[on/off]`, toggle them. This won't affect hotkeys on these hotbars, just which one to be displayed.
- `[Advanced]`Toggle 2 states.

### display
USAGE `/hotbar display [hotbar number] [on/off]`  

Change the visibility of specified hotbar. If omitting `[on/off]`, toggle them. Visibility do not affect the hotkey on it. If there are keybinds on hidden hotbars, you can still press them.  
- `[Advanced]`Use for Folding Menu Macro System. For more details, please read part 2.

Example of these two subcommands:
```
/hotbar share 1 off
/hotbar share 2 off
/hotbar share 3 off
/hotbar share 4 on
/hotbar share 5 on
/hotbar share 6 on
/hotbar share 7 on
/hotbar share 8 on
/hotbar share 9 on
/hotbar share 10 on
/hudlayout 1
/hotbar display 4 on
/hotbar display 6 off
/hotbar display 8 off
/e Combat Mod UI changed.
```

### set, action, general, pet, buddy, emote, item, mount, minion, marking, waymark, blueaction, etc. (We call them "sets")  
USAGE `/hotbar [sets] [name] [hotbar number] [slot number]`

Set the specified hotkey to specified location.
-  `[hotbar number]` can be replaced by "`current`" to specify the first hotbar. (mostly hotbar 1, changed when you have used `/hotbar change`) 
- Omit `[slot number]` and `[hotbar number]` to set on the first blank.
- If specify a slot that already has a hotkey, it will be overwritten.
- Cannot set on undisplayable hotbars.
- Note that this command won't be affected by anything except loading.
- Action hotkey set by this command can be queued in.
- You should input the full original name like `Verholy` => `Veraero`.
- NQ and HQ items are different, remember to copy the `HQ icon`.
- If specifying an upgradeable action, no matter which grade you specify, the highest grade you learned will be set.
- You cannot set actions from other classes/jobs.
- Subcommand general can mostly be replaced by set (set equals to action), except "`jump`", for DRG has an action which has the same name.  

Example:  
- Quickly set a bunch of hotkeys that are only used in a few occasions to the designated position.   
  ```
  /hotbar set "Egi Assault" 7 1
  /hotbar set Tri-disaster 7 2
  /hotbar set "Energy Drain" 7 3
  /hotbar set "Egi Assault II" 7 4
  /hotbar set "Egi Assault" 7 5
  /hotbar set "Dreadwyrm Trance" 7 6
  /hotbar set "Egi Assault II" 7 7
  /hotbar item "Grade 3 Tincture of Intelligence[HQ icon]" 7 8
  /hotbar set "Ruin III" 7 9
  /hotbar set Tri-disaster 7 10
  /hotbar set Fester 7 11
  /hotbar set "Ruin III" 7 12
  /e SMN TEA Beginner ready!
  ```
- [Advanced]Overwrite an executed action macro with action hotkey, allowing it to be queued in. For more details, please read part 2.
  ```
  /micon "Midare Setsugekka"
  /ac "Iaijutsu"
  /hotbar set "Iaijutsu" 1 8
  /s Facing the STORM!!!
  /wait 1
  /hotbar copy SAM 10 SAM 1
  ```

### remove
USAGE `/hotbar remove [hotbar number] [slot number]`

Remove the specified hotkey. You cannot remove hotkey on undisplayable hotbars. Input "`all`" at `[slot number]` will remove everything on this hotbar.

Example:
- Delete used macros which shouldn't be run twice. 
  ```
  There is no appropriate example here.
  ```
- Delete everything displayable (`rm -rf ./*`).
  ```
  /hotbar remove 1 all
  /hotbar remove 2 all
  /hotbar remove 3 all
  /hotbar remove 4 all
  /hotbar remove 5 all
  /hotbar remove 6 all
  /hotbar remove 7 all
  /hotbar remove 8 all
  /hotbar remove 9 all
  /hotbar remove 10 all
  ```

### change
USAGE `/hotbar change [hotbar number]`
  
Change the first hotbar to show the contents of specified hotbar while keep its keybind.
- `[hotbar number]` can be "`next`" or "`prev`", refers to current number +1/-1.
- Hotbar 1 is not changed though undisplayable.
- If you make change on the changed first hotbar, changes will apply to its source at once. 
- Shown hotbars will keep their share setting.
- Unable to change to undisplayable hotbars except `hotbar 1`.
  
Example:
- `[Advanced]`hotbar-change Macro Systems.
  ```
  It's hard to be shown. For more details, please read part 2.
  ```

### copy
USAGE `/hotbar copy [class/job name(abbr.) 1] [hotbar number 1] [class/job name(abbr.) 2] [hotbar number 2]`  

Copy the former specified hotbar to the latter one. 
- `[class/job name(abbr.)]` can be "`current`" or "`share`", which specify the current class/job or shared hotbar, separately.
- Almost nothing can prevent this except loading.
- You can specify any undisplayable hotbars.
- Anything on the latter hotbar will be overwritten.
- This is the only command that can create a macro hotkey(Unless Yoshida P add a "`/hotbar macro`" one day).  

Examples:  
- Backup current hotbars.  
  ```
  /hotbar copy BRD 1 BRD 4
  /hotbar copy BRD 2 BRD 5
  /hotbar copy BRD 3 BRD 6
  /e Backup complete.
  ```
- `[Advanced]`Set a macro hotkey to designed position.
- `[Advanced]`Use for Menu Macro System. For more details, please read part 2.
- `[Advanced]`Using in Advanced hotbar-change Macro Systems to achieve more function.

## Chatting Command
Most basic combat macros are aimed at sending massage to communicate. You can find all chatting command at https://na.finalfantasyxiv.com/lodestone/playguide/db/text_command/?category2=1. Here are only some notes.

Some public channels(say, yell, shout, emote) have `continuous messages restriction`. If you send more than 1 message in 1 second, the rest will not be seen by others. But they can still complete quests that need you say something. If you are too shy to made your message seen or tired of inputting same words in beast tribe daily quests, you can do like this:
```
/s _(:3rz)_
/s snae ling, Beaver, lali-ho, etc.
```

There are 2 special channels: emote and echo. You can use `/em` and `/e` to use these channels. Emote channel will show your name, but have no separator between name and message. Echo channel won't show your name, for only yourself can see it.

## Macro-controlling Text Command
  Macro-controlling text command includes `/wait`, `/macroicon`, `/macrolock`, `/macroerror` and `/macrocancel`. We have learned `/wait` above. The rest of them can write "`macro`" as "`m`" for short.

### /micon
```
ALIASES:
　/macroicon, /micon
USAGE:
　/micon "icon name" [category]
→Displays the specified icon as a hotbar icon. If used twice in a single user macro, only the first instance will be recognized.
>>Categories:
　action
　　If the icon name is an action, action recast time and required MP will be displayed with the icon.
　blueaction
　　If the icon name is a blue mage action, action recast time and required MP will be displayed with the icon.
　pvpaction
　　If the icon name is a pvp action, action recast time and required MP will be displayed with the icon.
　general
　　If the icon name is a general action, action recast time will be displayed with the icon.
　emote
　　If the icon name is an emote, its icon will be displayed.
　companion
　　If the icon name is a companion action, its icon will be displayed.
　pet
　　If the icon name is a pet action, its icon will be displayed
　minion
　　If the icon name is a minion, its icon will be displayed.
　mount
　　If the icon name is a mount, its icon will be displayed.
　enemysign
　　If the icon name is an enemy sign, its icon will be displayed.
　waymark
　　If the icon name is a waymark, its icon will be displayed.
　gearset
　　If the icon name is a gear set number, its icon will be displayed.
　classjob
　　If the icon name is a class or job, its icon will be displayed.
　quickchat
　　If the icon name is a Quick Chat message, its icon will be displayed.
Category defaults to action when none is specified.
```

This is used for decorate your macro and distinguish them. No one can find his wanted if hotbars are like this. 
![](img/micon.png)  
- If you specify an upgradeable action, no matter which one you specify, the highest grade you learned will be shown. If your current job cannot learn this action, it will be shown as the lowest grade.
- This command can correctly specify derivative action.
- If you want to specify an item, you must keep it in your inventory. Don't forget that HQ and NQ are different items. 
- The crafter action icon will automatically change. If you are not a crafter, icon will be shown as carpenter's.
- To distinguish macro from real hotkey, there will be a gear on the top right corner. ![](img/difference.png)

### /mlock
```
ALIASES:
　/macrolock, /mlock
USAGE:
　/macrolock
→Prevents the execution of any additional macros until all steps following /macrolock have been executed.
```
This command prevents interruption of important macros, but it also reduces its flexibility. It only protects the commands after it. If you want to interrupt a macro with macro lock, you can use `/mcancel` or "`Cancel Macro`" (This function doesn't have a default keybind).

### /merror
```
ALIASES:
　/macroerror, /merror
USAGE:
　/macroerror [subcommand]
→Display or hide text command errors within a user macro. Any errors are displayed upon macro execution. Setting resets to on after macro is executed.
>>Subcommands:
　on Displays error message.
　off Hides error message.
Toggle between on and off when no subcommand is specified.
```
Almost never use "`on`". This can prevent some error log when using complex target macro. Only macro error can be prevented, including logical target do not exist, cannot use at this time, command not exist and macrolocked. Cannot prevent action error like not ready yet, MP insufficient, target out of range and target not in sight.

### /mcancel
```
ALIASES:
　/macrocancel, /mcancel
USAGE:
　/macrocancel
→Cancel the currently executed macro. Cannot be used in a macro.
```
It can only be executed from chat window. If you put it in a macro, it has no effect while it can also interrupt macro without macro lock for execution of a blank macro.

## Examples
Here are some other useful text commands:
- `/? [text command]`: use this to get text command usage.
- `/gs change [gear set number/name] [glamour plates number]`: Change your gear set and your glamour if available. [glamour plates number] can be omitted.
- `/hudlayout [HUD number]`: change your HUD layout to specified number. Omit number will open the `HUD Layout` setting.
- `/ta [placeholder]`: target the logical target.
- `/mk [mark name] [placeholder]`: mark the specified mark to logical target. Mostly used in frontline.
- `/waymark [mark name] [placeholder]`: mark the specified mark at the feet of logical target. Mostly used in frontline.
- `/facetarget`: face target.
- `/automove [on/off]`: automatically forwards.
- `/nt`: target the rightest enemy in your sight.
- `/tenemy`: target the nearest enemy in your sight.
- `/tlt`: target your last target.
- `/tle`：target your last targeted enemy. If you are targeting an enemy, nothing will happen.
- `/busy [on/off]`: be busy.
- `/battleeffect [self/party/other] [all/simple/off]`: Change your battle effect setting, preventing you from overwhelmed by battle effects. Omit `[all/simple/off]` will toggles between all and off.
- `/playtime`: show how long time you are online.
- `/title set [title]`: change your title. You can add this to job changing macro.
- `/shutdown`: shutdown FFXIV.

Here are some other useful macros:
- This macro can be a better "`Tab`", for it can help you retarget your enemy after healing party members or attacking adds, regardless the field of vision.
  ```
  /merror off
  /nt
  /ta <le>
  /micon "Target Forward"
  ```
- This macro can let all your pet, minion and chocobo away, and also turn off all battle effects. Use this when too many players in battle like hunting.
  ```
  /micon Succor
  /merror
  /pac Away
  /cac Withdraw
  /minion
  /battleeffect party
  /battleeffect other
  ```
- This macro let you summon your mount. If unable to summon, it will automatically change to "`sprint`". If you want to sprint at mountable area, just pressing with a jump.
  ```
  /micon Sprint
  /mount Snowman (change this to anything you like)
  /ac Sprint
  ```

## Debug
It would make everyone upset when your new macro doesn't work without reason. Actually, there are so many reasons can be. A text command has a main command started with a "`/`". It may have many sub commands, numbered by spaces.

Remove any "`/merror`", and retry. Error log will tell you what's wrong. Here are some common errors:
- Spelling error. You'd better use auto-translate to make a check.
- Spaces missing. Each two sub commands should split by spaces. Especially attention on "`[job name] [number]`". Missing spaces will let system find a job names like "`SCH1`" instead of "`SCH`" and result in invalid name.
  
If still no error log but macro actually doesn't work, things can be complex. Check what has happened. Sometimes you think nothing happen but changes happen at corner you can't see. Here are some common errors:
- Actions cast on error target: think about command delay and sequence.
- "`/hotbar change`" to an error hotbar: check share setting.
- "`/hotbar copy`" clear your hotbar: check share setting.
- action after "`/wait`" do not execute: check interruption or longer the wait time.
- "`/micon`" doesn't work: check category and name. For item, check HQ icon and possession.

## Conclusion
After reading this part, you should have learned:
- How to use macro panel
- Basic principle of macro
- Independence and objective existence of hotbar
- Distinguishing macros that significantly reduce your DPS
- Important text command
- Writing simple macro

This is the ending of Part 1. If you read carefully, you will no longer need to ask for macros. You should be able to write any macros you can copy and paste. The more advanced macros cannot be simply copied and pasted. If you are longing for advanced macros, go on reading Part 2. If you meet something unknown, you can go back to Part 1 to find the answers, or just give it a try!

# Part 2 Advanced Macro
## Introduction
From here you will go into advanced macros. For reducing pages, there will be some abbreviations. If you meet something unknown, go back to find the explanations. 

Advance macro is based on keybind. You may press so many keys to cast a lot of actions before, but what macros do is setting the hotkeys you may need to your preferred keys. The operation with macros may be extremely different, so you'd better forget your common sense. Of course, I do not mean using macros must be better. This is just an alternation.

Instead of focusing on how to do, I'll put more words on why. **You can hardly learn something by copying and pasting.** Only your creativity grants you the best macro. Advanced macros also have their disadvantages. We will also talk about chooses between disadvantages. Nowadays we prefer using more hotbars instead of macros, for macro panel slots are extremely limited. There is no absolutely perfect macro, but you can find your own perfect.

## FAQ
>- Q: Is there any macros I can copy and paste?
>- A: Hardly any. Macros serve issues. If you want to ask for macros, you must clarify what issues you want to solve first. Here will be some examples, but you cannot copy and paste directly. You must customize them before using. You can also develop your own macro based on these imperfect examples.

>- Q: Does game controller suit Macrology?
>- A: Of course. This guide mostly uses /hotbar just because I play on keyboard and mouse. You can use /chotbar in the same way. There are some advantages but also disadvantages compared to keyboard.

>- Q: TL; DR.
>- A: Advanced macros are complex. If you cannot bear this length, you cannot write good macros. In fact, macros are just complex, not difficult. Give it a try, and you will learn a lot. Experienced macrologists can understand most macros at first glimpse, and write a brand new macro system in no more than half an hour.

>- Q: Many players said using macro will damage my DPS, and sometimes it doesn't work.
>- A: Most of them have only used basic macros which have a lot of /ac. Action casted by them cannot be queued in, which damage their DPS. You could just ask them: Why? Have you thought how to avoid? Have your heard Macrology?

>- Q: There are also /ac in your macros, so your macros will also damage your DPS.
>- A: "/ac" itself doesn't damage your DPS. It's actions cast by /ac that damaging your DPS. If this /ac doesn't cast an action, or your GCD is already ready, there will be no DPS loss. By the way, there are some ways to reduce GCD loss due to /ac.

>- Q: Why my macro doesn't work?
>- A: It works, but not as you want. Find out what happened. "Doesn't work" makes no sense.

>- Q: When network is poor, macro will make things a mass.
>- A: All macros are executed on local. Only those with "/wait" will go wrong. You can give them a longer wait time, or find a way to avoid waiting.

>- Q: My hotbar is not enough to use advanced macros.
>- A: I don't think you can use up 390 hotbars before 200 macro slot use out. Use your hidden hotbar better.

>- Q: I want to make things easier by macros, but why it seems more complex?
>- A: When you are making a macro system, it's complex. But when you are in combat with your macros, it will be easier. Everything is in balance. if you want something easier, there must be something else more complex. In fact, it just because of a lot of commands, but the logic is simple. 

>- Q: Macro is fixed but situation can change.
>- A: Changes are predictable. Add some alternation to your macros.

>- Q: Misoperation will break the macro system.
>- A: Misoperation will also break your rotation without macro. Macro is aimed for reducing your possibility to misoperation in rotation.

>- Q: Why don't you use the time you cost on macro to practise on striking dummy?
>- A: Why don't you use the time you cost on keybind and HUD Layout to practise on striking dummy? A better keybind and HUD Layout will reduce your time cost on mastering your job right? Macro is the same. Time cost on macros will reduce the time needed to master your job. On the other hand, writing good macros need deep knowledge of rotation. When you writing macros, you are also learning your rotation at the same time.

>- Q: You need macros for such a simple job?
>- A: Macros serve issues. You may not think it an issue, but someone else may.

>- Q: I can play well without macros already. Is there anything else I can get from Macrology?
>- A: You may make it easier to play as well or even better. Macrology is a way of thinking, which can be applied in all aspects, not only to simplify the operation, but also to do all kinds of planning. If you can cost less attention on your rotation, you will have more attention to deal with gimmicks and even lose less GCD.

>- Q: Macrology serves beginners or experienced players?
>- A: Anyone who wants. Where there is an issue, there can be a macro. Macrology can help you breaking the ranking, ease the difficulty, or even just for fun.

>- Q: Why you love macro so much?
>- A: Macro is one of the most interesting ways to play the game. Macrology is an exploration of possibility and a challenge to the game system, which makes me happy. The producer add a lot of limits on macro, which makes it hard to use, so there are also some players think that macro is useless. But there's nothing useless. Macro is actually useful, just a little complex. It's too useful so that the producer has to limit it.

## Abbreviation
For reducing the pages, we define some abbreviation here:
- `Operation hotbar`: the hotbars you mainly use.
- `Sub hotbar`: the hotbars you do not use directly, but accessed by /hotbar.
- `Base hotbar`: the hotbars you store your original hotbars. We use these hotbars to reset changed operation hotbars.
- `Interchange hotbar`: a more advanced base hotbar, for changing hotbars before copy without affecting base hotbar.
- `Monitor`: an operation hotbar that do not store something but always ready to show something copied.  

**Note that they are all normal hotbars.**

- "`sets`": `/hotbar (set/emote/pet/minion...)`, a sets of set-like sub command.
- `turn to X`: copy hotbar X to monitor.
- `Preinstall`: store hotbars to base hotbars before using.
- `Reset`: copy the original hotbars to operation hotbars.
- `Backup`: copy hotbars to a base hotbar when using.

## Message Macro Type ASWC
We once talked about how to prevent an action macro with message filling the scene: `/ac`, `/wait 1`, message. This made action cannot be queued in, and message will be late. We have to repeatedly press this macro to ensure the casting of action, due to `/ac`.
  
For a better choice, we must solve an issue: queue in this action. Only action cast by normal hotkey can be queued in, so we must create an action hotkey. `/hotbar set` can do this. We use `/hotbar set` to overwrite this macro. When we press this macro, message will be sent, then macro is overwritten by the true action hotkey. Press it one more time, queue in this action. **Note that you must press twice, or action will not be cast.**

Issue solved, but a new issue comes: macro has been overwritten. We need a way to reset the macro back. Only `/hotbar copy` can create a macro. Before we run this macro, we can backup this hotbar to a base hotbar, and copy it back after run. To ensure the time you need to press the true action hotkey, we need to wait 1-2 seconds. 
  
Let's have a review: 
1. press the macro 
2. backup hotbar 
3. action hotkey set 
4. message sent 
5. press again 
6. queue in action 
7. 1-2 seconds later 
8. hotbar reset

Finally, if the action is already ready, there will be a time loss between pressing twice. So we can add `/ac` at the head. This is not essential, and sometimes reduce the flexibility of macro. You can delete it if you think it damage your DPS, though it may actually increase your DPS.

This macro now holds commands of `/ac`, `/hotbar set`, `/wait`, `/hotbar copy`, abbreviated as `ASWC`. We will see it later in many forms. Let's see a example:
  (`PLD 4` is an empty hotbar, `Hallowed Ground` macro is set on `PLD 3, slot 8`.)
```
/micon "Hallowed Ground"
/ac "Hallowed Ground" (delete this line if needed)
/hotbar copy PLD 3 PLD 4 (backup)
/hotbar set "Hallowed Ground" 3 8 (set the real action hotkey)
/p I AM IMMORTAL!!! <se.1>
/wait 1
/hotbar copy PLD 4 PLD 3 (reset)
```
And here is a frame by frame analysis: 
1. We start from here, press the `Hallowed Ground` macro   
![](img/aswc1.png)  
2. due to animation lock, `/ac "Hallowed Ground"` cannot cast action 
3. `/hotbar copy PLD 3 PLD 4` backup `PLD 3` 
4. `/hotbar set "Hallowed Ground" 3 8` set the real hotkey of `Hallowed Ground` 
5. `/p I AM IMMORTAL!!! <se.1>` is sent:  
![](img/aswc2.png)  
6. Now press it again:  
![](img/aswc3.png)  
7. `Hallowed Ground` active. `/wait 1` 
8. `/hotbar copy PLD 4 PLD 3` reset the hotbar:

GIF:  
![](img/aswc.gif)

There are two more conditions to discuss:
- If you need to run other macro in the time of `/wait 1`, this macro will be interrupted and hotbar cannot be reset. You can add this reset command to all macros which can be used here, or add to another macro which is frequently used in combat. You can also replace the `/wait` with some nonsense command, lower your FPS, and use your fastest speed to press twice in command delay.
- This macro cannot cast action on logical target. If you need to, you can add `/ta <logical target>` at the head, and `/tlt` at the tail. You may lose some auto-attack due to this target change.


## Action State-system
Character has many "`action states`". Some are defined by game system, and others are artificially defined. In an action state, there should be actions you should cast, and actions you should not cast. For example, you cannot cast `Fire IV` in `Umbral Ice`, and shouldn't cast `Fire`. You shouldn't cast `Yukikaze` or `Gekko` after `Shifu`. To prevent casting the wrong actions, and making it easier to cast the right actions, we can temporarily remove these wrong actions and move the right actions to a better position. This calls an action state-system. The following macros are made by this system.

## hotbar-change Macro System
hotbar-change macro system is a well-known macro system (maybe). Each action state is stored in a base hotbar. By "`/hotbar change`" command, they can take turns using the keybind of the first hotbar. We need to solve just one issue: how to detect action state change.

Except combo time out, all changes of action states are from action. We can bind this command in action macro. I do not means "`/ac`". We should queue in this action. We need a true action hotkey. But this time we needn't use "`set`". Hotbar will change when macro runs, so we just need to put an action hotkey on the same slot of the hotbar we change to.

Let's have a review: 
1. press the macro 
2. hotbar change 
3. press again 
4. queue in action

Also, you can add "`/ac`" at the head to prevent time loss between press twice when action already ready.

Here is an example:
```
/micon Shifu
/ac Shifu (delete it if you want)
/hotbar change 6
```

It's so simple. The thing complex is your logic. You should clarify what you should and shouldn't do in this action state, and give them a suitable keybind. In the example below, I put this macro on `hotbar 1, slot 2`. On `hotbar 6, slot 2` is the true `Shifu` hotkey. `slot 3` is `Kasha`. No `Jinpu`, `Gekko` or `Yukikaze` on this hotbar. To start a new combo after `Kasha` or combo break, a `Hakaze` macro which holds "`/hotbar change 1`" is put on `slot 1`. Other action hotkeys are copied and unchanged. This is another action state of "`after Jinpu`":  
![](img/hc1.png)  
You should `preinstall` all states. SAM has seven states when combat with single target: "`after Hakaze`", "`after Shifu`", "`after Jinpu`","`after Gekko`", "`after Kasha`", "`after Yukikaze`" and "`after Meikyo Shisui`". Some states are similar, so we can merge them.   
Finally we have "`after Shifu`", "`after Jinpu`", "after `Meikyo Shisui`" and "`beginning`" states. 
- "`beginning`" state has `Hakaze`, `Yukikaze`, `Shifu` macro and `Jinpu` macro. 
- "`after Shifu`" state has `Hakaze` macro, `Shifu` and `Kasha`. 
- "`after Jinpu`" state has `Hakaze` macro, `Jinpu` and `Gekko`.
- "`after Meikyo Shisui`" has `Hakaze` macro, `Kasha`, `Gekko` and `Yukikaze`. 

There should be at least 4 macros: `Hakaze` macro, `Shifu` macro, `Jinpu` macro and `Meikyo Shisui` macro. If you want to use `Shifu` and `Jinpu` in `Meikyo Shisui` or add AOE actions to this system, further adjustment and more macros are needed. Here is a final scene: (`Meikyo Shisui` macro is not shown)  
![](img/hc2.png)  
(`Question`: How to modify this to cast `Mangetsu` and `Oka` after `Meikyo Shisui`?)
  
Let's see a frame by frame analysis:  
1. I press the `Shifu` macro, but GCD is not ready, so "`/ac Shifu`" cannot cast action.
![](img/hc3.png)  
2. Then "`/hotbar change 6`" successfully change my hotbar:  
![](img/hc4.png)  
3. And I press again. Though GCD is still not ready, `Shifu` is queued in:  
![](img/hc5.png)  
4. Without one more pressing, `Shifu` is cast by action queue:  
![](img/hc6.png)  

GIF:  
![](img/hotbar_change.gif)

Though named "`hotbar-change macro`", "`change`" is not an ideal command. "`change`" is intuitively visible and easy to modify, but cannot use undisplayable hotbars. You have only 10 displayable hotbars. "`hotbar copy`" is a better choice. You can store your action states to undisplayable hotbars, and release your displayable hotbars for other usages. Here is an example:
```
/micon Shifu
/ac Shifu
/hotbar copy SAM 6 SAM 1
```
Almost unchanged. But note that `hotbar 1` can no longer store anything. It has become a `monitor`. When you "`after Shifu`", `hotbar 1` will show the things on `hotbar 6`, but you cannot change it directly. You should copy it back to `hotbar 6` to apply your change. For this reason, "`copy`" will cost one more hotbar. If you are annoyed about this, you can add a backup command, though it cost more macro slots.

The advantages of "`change`" are direct modification and intuitively visible, while the advantages of "`copy`" are more accessible hotbars and more advanced usages.

Here is a special situation: in different action states, the same action has different functions. For example, `Transpose` swaps `Astral Fire` with a single `Umbral Ice`, or `Umbral Ice` with a single `Astral Fire`. We need two macros, but we don't want an action to occupy 2 hotbar slots. So we need a little trick. To ensure the cast of `Transpose`, we need it be normal hotkey, but macro later. We can backup the target hotbar, and "`set`" after "`change`" (note that hotbar number may change). Wait a little, and reset it. If you use "`copy`", backup is not needed for it has been preinstall.

- "`change`" type:
  ```
  /micon Transpose
  /mlock
  /ac Transpose
  /hotbar copy BLM 6 BLM 10 (backup)
  /hotbar change 6
  /hotbar set Transpose 6 5
  /wait 1
  /hotbar copy BLM 10 BLM 6
  ```
- "`copy`" type:
  ```
  /micon Transpose
  /mlock
  /ac Transpose
  /hotbar copy BLM 10 BLM 1
  /hotbar set Transpose 1 5
  /wait 1
  /hotbar copy BLM 10 BLM 1
  ```

Don't you think it looks like `ASWC`? In fact, this is a compound of `ASWC` and `hotbar-change` macro. You will see this trick in more advanced macros. There are also issues about interruption and reset we once talked. You can also use "`share`" or "`rolling macro`" to solve this situation, which is more advanced. I'll talk about them in `Part 3`. If you want to challenge yourself, think about how to exchange different drinks in two bottles.

## hotbar-change Macro System Logic Guide Diagram
It's proved so hard for beginners to develop a reasonable logic of `hotbar-change` macro system. Here are a guide diagram:
1. make a debug mode. Create a new HUD Layout setting, then arrange hotbars neat. Display all hotbars. Turn off all shared hotbars. Show unassigned slot, and display hotbar numbers in `Character Configuration`. You can write a macro to make it faster:
    ```
    /hotbar share 1 off
    /hotbar share 2 off
    /hotbar share 3 off
    /hotbar share 4 off
    /hotbar share 5 off
    /hotbar share 6 off
    /hotbar share 7 off
    /hotbar share 8 off
    /hotbar share 9 off
    /hotbar share 10 off
    /hudlayout 3
    ```
    ![](img/hcg1.png)

2. think about your wanted shape of hotkeys. Clarify the usage of every hotbars. Remember to think about how to jump to other combos, and keep them in the same slots.
    - `Hotbar 4` is the state of "`in single target combos`". `Atonement` will break your combo so remove it.
    - `Hotbar 5` is the state of "`after combos`", `Atonement` maybe available. To begin another combo, you must cast `Fast Blade` first, so remove `Riot Blade`.
    - `Hotbar 6` is the state of "`in AOE combo`". You can also cast `Atonement` if still any stacks left. Draw some arrows to show your rotation.  

    ![](img/hcg2.png)

3. For every action on the tail of vertical arrows, write a macro which holds "`/hotbar copy current [hotbar number of arrow's head] current [operation hotbar number]`". For this example, they are:
    ```
    /micon "Fast Blade"
    /ac "Fast Blade"
    /hotbar copy current 4 current 1

    /micon "Royal Authority"
    /ac "Royal Authority"
    /hotbar copy current 5 current 1

    /micon "Goring Blade"
    /ac "Goring Blade"
    /hotbar copy current 5 current 1

    /micon "Total Eclipse"
    /ac "Total Eclipse"
    /hotbar copy current 6 current 1
    ```  
    ![](img/hcg3.png)

## Combo Macro System Type ASWC
Before `Stormbloods`, PVP shares almost the same actions with PVE, including combos. But when `Stormbloods` refactors PVP actions, it makes a combo hotkey. By one key you can access to the whole combo, never mistake. Can it be done in PVE by our own hands? Of course, but also complex.
  
All we need is changing the combo state, which is an action state. We can use the frame of `ASWC`, just changing the last "`reset`" to "`turn to next state`".
  
Let's have a review: 
1. press the macro 
2. action hotkey set 
3. press again 
4. queue in action 
5. 1-2 seconds later 
6. change to next state.
  
Example: (this macro is on the `hotbar 1, slot 4`, `hotbar 5` holds a "`Vorpal Thrust`" macro at the same slot)
```
/micon "True Thrust"
/mlock
/ac "True Thrust"
/hotbar set "True Thrust" 1 4
/wait 1
/hotbar copy DRG 5 DRG 1
```

Also, you should `preinstall` these macros like this:  
![](img/ac1.png)

Let's see a frame by frame analysis:  
1. We start from here, press `True Thrust` macro:  
![](img/ac2.png)  
2. GCD is ready so it cast immediately.  
![](img/ac3.png)  
3. After 1 second, `/hotbar copy DRG 5 DRG 1` runs, and change the hotbar to next state.  
![](img/ac4.png)  
4. I press this new macro, GCD not ready so no action cast but action hotkey set.  
![](img/ac5.png)  
5. Press again, queue in this action.  
![](img/ac6.png)  
6. Action cast by action queue.  
![](img/ac7.png)  
7. 1 second later, next state comes.  
![](img/ac8.png)  

GIF:  
![](img/aswc_combo.gif)

Looks easy, but there are a lot of difficulties. Every combo action needs a macro, which cost a lot of slots in `macro panel`. And if you make some mistakes in operation, you will pay a **high price** for it.

You must control your keyboard pressing. Starting pressing rapidly when cooldown is above 1 second or keep pressing rapidly more than 1 second will both result in state change without action cast. Add `/wait 1` at the end may help, but cannot completely solve this. If this mistake actually happens, you need a "`return to previous state`" macro or an alternate hotkey. 

To reduce macro panel cost for "`return to previous state`" macro, we can use `interchange hotbar` like this:
```
/micon [Any combo action]
/mlock
/ac [Any combo action]
/hotbar copy DRG 1 DRG 7
/hotbar set [Any combo action] 1 4
/wait 1
/hotbar copy DRG [next state hotbar number] DRG 1

/e This is "return to previous state" macro, DRG 7 is interchange hotbar
/hotbar copy DRG 7 DRG 1
```
For these reasons, if you like pressing keyboard again and again, I advise you not to use this combo macro. **It really tolerates no mistake**. You must press just twice when GCD about to ready, and ensure you can cast this action(I mean target out of range or target lost). You should also master the way of "`return`".

As for combo time out, you may want to add `/wait 15` then "`return to first state`", but you have to remove your macro lock for this, this is what I suggest not.

## Exhibition Macro
There are some jobs holding a complex but fixed rotation. When it come across with complex gimmick, it's easy to make mistakes. You may have seen some players put a rotation like this:    
![](img/e1.png)(from patch 5.1)

Click from left to right, and you perfectly complete your rotation. But what if your mouse is busy? And don't you think it obstruct the view? We can use exhibition macro to make it better.

You need `backup` your operation hotbar first, and `preinstall` your rotation, then make 3 simple macros like this:   
![](img/e2.png)  

- The macro on hotbar 6 is used to start rotation and begin to cast Ruin III before pull.
  ```
  /micon "Ruin III"
  /ac "Ruin III"
  /hotbar copy SMN 7 SMN 1
  ```
- The one on hotbar 7 is used to change to next state (because 1 hotbar is not enough for this rotation)
  ```
  /hotbar copy SMN 8 SMN 1
  ```
- The one on hotbar 8 is used to finish rotation and go back to normal hotbar.
  ```
  /hotbar copy SMN 6 SMN 1
  ```

GIF:  
![](img/exhibition.gif) 
  
Seems easy but bear in mind that **every sword of macro has two edges**. Your rotation will be completely fixed, so you'd better also master the rotation by your own hands. If situation changes, don't use this macro. If changes are predictable, You can also make an alternation macro.

Tips: Use secondary keybind and you can still rolling `1234567890-=` instead of `12345qergv~f`.

## Menu Macro System
pass

## Conclusion
pass