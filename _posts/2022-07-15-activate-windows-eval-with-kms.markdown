layout: post
title:  "Activating Windows Server Eval Edition with KMS"
date:   2022-07-14 00:30:00 -0600
author: Leo
categories: windows

Recently I needed to install *Windows Server 2019* on a couple of bare metal servers. I didn't want to go through the trouble of figuring out what credentials I needed to sign in to the company's Volume and Licensing Center account so I figured I could just download an eval edition copy of the ISO and figure out the rest later. So here is the rest.

## Get the KMS key

For a computer to activate with KMS, first it needs to have the right key installed. This is called the **KMS Client Key** and usually you don't need it except when you downloaded and installed the evaluation edition of *Windows Server*.

We can grab the key from [**this**]("https://docs.microsoft.com/en-us/windows-server/get-started/kms-client-activation-keys") site, make sure to get the one that matches your version of Windows. For **Windows Server 2019 Standard** it will look something like this:

> N69G4-B89J2-4G8F4-WWYCC-J464C

## Use DISM to change the edition and product key

The docs for KMS uses a different command that didn't work for this scenario so instead I followed the steps on the doc for **DISM**. The DISM command will change the eval key to the KSM Client Key and change the edition all in one go. 

```powershell
DISM /online /Set-Edition:<windows edition> /ProductKey:<KMS Client Key> /AcceptEula
```

Once you're prompted to restart say yes and once it boots back up the OS should be fully activated through the network's KMS host.

Read more about DISM from [**here**]("https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/dism-windows-edition-servicing-command-line-options?view=windows-11")