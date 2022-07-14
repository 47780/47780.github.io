---
layout: post
title:  "PowerShell Bits #01"
date:   2022-07-14 00:30:00 -0600
author: Leo
categories: powershell
---

Once again, the whole purpose behind this site is to generally minimize the amount of times I have to google the same things again and again. So, to help my limited memory, I'm starting a series were I jot down quick *PowerShell* commands I put together that I know I'll be using again later.

This first entry will cover a couple commands I put together when I needed to create several groups at once and also add users to these groups. There are probably prettier ways of doing this but, I am a big fan of quick and dirty when it comes to small one off scripts like this.

## Creating groups in bulk

I had a list of 8 groups that needed to be created, all under the same OU so we'll just start with an array for the names.

```powershell
$group_list = @(
	"Security_Group-1",
	"Security_Group-2",
	"Security_Group-3",
	"Security_Group-4",
	"Security_Group-5",
	"Security_Group-6",
	"Security_Group-7",
	"Security_Group-8"
)
```

Next I put together the command to create these groups, they are all the same type and scope so we can keep it simple.

```powershell
New-ADGroup -name <group name> -GroupCategory Security -GroupScope Global -Path "OU=Security,OU=Groups,DC=ad,DC=catorce,DC=uno"
```

Then we just need to throw it all in a `foreach` loop and we're done.

```powershell
foreach ($group in $group_list) {
	New-ADGroup -name $group -GroupCategory Security -GroupScope Global -Path 		"OU=Security,OU=Groups,DC=ad,DC=catorce,DC=uno" -whatif
}
```

Just to make sure I don't make a mess, I usually thrown in a `-whatif` to see that things run without errors before pulling the trigger. If everything clears we can just go back and take off that flag and let it create the groups. 

Finally, just to check everything was created properly we can just check for the contents of that OU.

```powershell
Get-ADGroup -Filter 'name -like "*"' -SearchBase 'OU=Security,OU=Groups,DC=ad,DC=catorce,DC=uno' | select name
```

## Adding users to a group

Next, lets add a list of users to a group. Same process, make an array of users and then use a `foreach` loop to add them all at once. 

In this scenario I only have the first and last name of the users. Ideally I'd prefer to use `SamAccountName` or another identifier that is unique to avoid mistakes but since it wasn't a lot of users and I needed to get this done quickly I'm just using the names to identify the users.

```powershell
$user_list = @(
	"Lopez, Vanessa"
	"Appleseed, John",
	"Smith, Mario",
	"Dominguez, Ana"
)
```

Just to check all users return the right object when filtered let's just pull them up with a loop.

```powershell
foreach ($user in $user_list) {
	Get-ADUser -Filter {name -like $user} | select name, samaccountname
}
```

Then once we've confirmed we're pulling the right objects we can edit the same loop to add the users to the group they need to be in. To save time I am nesting `Get-ADUser` inside the command and pulling `SamAccountName` from it to pass on as the input for `-Member`.

```powershell
foreach ($user in $user_list) {
	Add-AdGroupMember -Identity "CN=Security_Group-1,OU=Security,OU=Groups,DC=ad,DC=catorce,DC=uno" -Members (Get-ADUser -filter {name -like $user}).samaccountname -whatif
}
```

Then we just need to confirm and we're all done!

```powershell
Get-ADGroupMember "CN=Security_Group-1,OU=Security,OU=Groups,DC=ad,DC=catorce,DC=uno"
```

