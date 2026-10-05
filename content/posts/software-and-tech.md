+++
date = '2026-09-24T17:49:38-04:00'
draft = false
title = 'Software & Tech I use'
+++

- **Distro:** NixOS
- **Laptop:** Thinkpad T14s Gen 2a
- **Editor:** Constant switching between Emacs and Vim, but I prefer Emacs for big projects
- **Window Manager/Ricing:** niri + waybar

## Laptop Troubles

I had the Acer Aspire A315-44p for about 2.5 years, but the terrible build quality was too much to handle. I had large cracks on my chassis, some keys on the keyboard started malfunctioning, and the final straw was my second RAM slot not working, even with the surface-level fixes that people try on them.

I bought this laptop thinking specs matter more than build quality, but over time I realized you do not have to sacrifice specs for build quality when you look at the refurbished laptop market. You will find business-grade 6 year old Thinkpads that were once thousands of dollars and are now in the hundreds on online marketplaces and can easily upgrade or modify anything that you do not want.

## Distro hopping history

My first distro ever was Lubuntu, which I installed on an old laptop after I saw PopOS took too much resources. Then I went on the Luke Smith youtube binge phase where I went Manjaro->Arch->Artix->VoidLinux and then stayed with VoidLinux as my main system while experimenting with Alpine and Kiss Linux.

I believe VoidLinux was the most comfortable distro I used on this old laptop due to the minimality of the distro and xbps-src. Alpine and Kiss were too minimal, and needing to compile too many programs took too many resources from my laptop. However, there were definite drawbacks, like xbps-src not being as big as the AUR or nix-packages, having to fix random bugs due to mismatches between my compiled xbps-src programs vs the libraries, and new programs requiring too much work to install.

Once I got a device with more specs, I switched to NixOS, as I was tired of having to reinstall everything by hand everytime I used a new device or messed my system to the extent that it wasn't fixable. NixOS required some work, but with how easy AI has made, writing Nix configs is effortless.

I love that now I can try even packages the AUR doesn't have and could easily contribute my own packages to nix-packages with a functional language like Nix. My projects faustlsp and faustfmt also got on nix-packages thanks to [magnetophon](https://github.com/magnetophon)!

For the past 1.5 years, I've been satisfied with NixOS despite all the quirks it has. I do not think I will be switching to anything else for a while now.
