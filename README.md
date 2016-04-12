# Galaban's Do Then plugin
This is a plugin for the Shattered Isles mud.

The purpose of this plugin is to add a "do" and "then" command to the mud for repeating or delaying crafting actions.  A "wait" command can be used as part of that processing.

     do <count> <command>   - repeat the command N times
     do                     - clear the "do" command
     then <command>         - Execute the command after the completion of the next crafting command
     then                   - clear the "then" command
     stop                   - clears both the "do" and "then" commands
     wait <delay in sec.>   - This adds a delay within the "do" or "then" command

### Specifics

The "do" command can be used to repeat a given craft command a given number of times.  The "then" command will execute

Entering "do" with no arguments will clear out the current "do" command.  Enter "stop" will clear both the "do" and "then".

The "then" command will execute after the current crafting action is completed.  If there is a active "do" command, though, it will wait until that is complete.

For example:

     chop;then gather poplar
     
This will send the "chop" command and then, after completion, send "gather poplar"

     do 5 chop;then gather poplar
     
This will send 5 "chop" commands (waiting for each completion) before sending "gather poplar"

### The Stack Character

The stack character can be used within the do/then commands to stack additional commands to be executed.  For the "do" command, you have to escape the stack command by enterring it twice.  For example:

     do 5 get all.poplar;;chop

For the "then" command, the stack character has been overridden to allow for multiple "then" commands to be stacked.  Because of this, you do not have to escape the stack command.  Once a "then" command has been found in the current command line, any commands that occur after that are part of the "then" command.  For example:

     then chop;then chop;then bundle poplar;get poplar
     do 5 chop;;then bundle poplar;get poplar
     
Notice in the second example, the standard escaping must occur.  However, once the "then" command is encountered, the stack command becomes part of the "then"

### Examples

     do 5 chop
     
This will execute the chop command 5 times

     then bundle poplar
     
Delay the "bundle poplar" command until after the next crafting command is complete (ie, chop)

     then get roasted pot;ne;wait 1.5;sell roasted;wait 1;sw
     
The "wait" command can be added to delay the rest of the "then" or "do" command.  

     do get steamed pot;;get 1 salt;;put salt pot;;get 1 rice;;put rice pot;;cook pot

This gets the results of the previous cooking ("steamed") from the pot, then restocks the pot and cooks it again.
