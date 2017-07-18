# License: AGPL-3.0+ with additional permissions

This software is released under the terms of the [GNU Affero General Public License, Version 3][AGPL-3.0+] (or at your option, any later version.)

## Grant of Additional Permission

The purpose of this Exception is to allow distribution of the files typically output by this software under terms of the recipient's choice.

You have permission to propagate output of this software, even if such propagation would otherwise violate the terms of AGPLv3. However, if by modifying this software you cause any non-template part of the version you received to be output from your modified version, then you void this Exception for the resulting covered work. If you convey that resulting covered work, you must remove this Exception in accordance with the second paragraph of Section 7 of AGPLv3.

The output of this software is typically written to a file named `.context`.

## Plain-Language Summary

You don't need to be concerned with license compatibility when you use `incontext` to manage the environment of any other code; the license of `incontext` has no effect on that code.

You can even distribute copies of `incontext` (under the terms of the AGPL) along with your project to others; the terms of the AGPL do not affect the project. This is considered an _aggregate_ of projects.

`incontext --init` outputs a script normally named `.context`. You can do anything you like with the `.context` script; the terms of the AGPL do not apply to it, because of the grant of additional permission made above. 

Given that permission, someone might consider a clever loophole: modifying `incontext` to output all of itself into the `.context` file, thereby creating a version of itself not covered by the AGPL. So the license tediously states that no, you are not allowed to do that nasty thing.

If you redistribute `incontext`, modified or verbatim, it must remain AGPL-licensed.

If you _combine_ some or all of `incontext`'s code into other software and distribute that, the entire thing must be AGPL'd.
"Combine" means you directly use or invoke the code from some other code, or vice versa.

If you somehow modify `incontext` to run as a network service, or incorporate parts of `incontext` into a service, you still have to release all the code to your users under the AGPL.

For example:

- You might use `incontext` to manage the environment settings for your proprietary software project.

- You might license copies of that project to people under whatever terms you choose. You may even include `incontext` in the software download to manage the project's environment. You must include or make the source code available for `incontext` under the terms of the AGPL, but your project's license and source code remains unaffected.

- You might decide to open-source that project. You may still apply whichever license you like; the license of `incontext` has no effect on it.

- You might modify the `.context` file for your project to start a database, call an API, detect and activate `rbenv` environments, and several other useful things. Those changes remain your own, and you may keep them proprietary or redistribute them alone or along with your project under whichever license you wish.

- You might decide that it would be more convenient to not have to add features to the `.context` file for every new project you create; instead, you modify `.incontext` to output an improved `.context` file. This change falls under the terms of the AGPL. If you convey it to anybody, it must be under the terms of the AGPL.

[Michael F. Lamb]: http://datagrok.org
[AGPL-3.0+]: http://www.gnu.org/licenses/agpl.html
