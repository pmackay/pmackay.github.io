---
layout: post
title: Working with Wikidata CLI
comments: true
---

Wikidata is an amazing open data project. I sporadically work on a variety of edit tasks, either adding items or cleaning up class and instance hierarchies. Recently I've been experimenting with the excellent [wikidata-cli](https://github.com/maxlath/wikidata-cli) and [wikidata-taxonomy](https://github.com/nichtich/wikidata-taxonomy) tools as a quicker way to browse and edit content.

I've been looking at the sharing economy recently (part of background research related to Metroflows):

```
> wd search sharing economy
Q2277143   sharing economy economic and social systems that enable shared access to goods, services, data and talent
```

A summary can be retrieved:
```
> wd summary Q2277143
Label sharing economy
Description economic and social systems that enable shared access to goods, services, data and talent
instance of (P31): economic system (Q273005)
```

And a set of claims:
```
> wd claims Q2277143
instance of (P31):            economic system (Q273005)

part of (P361):               circular economy (Q497743)

topic's main category (P910): Category:Sharing economy (Q22712119)

BnF ID (P268):                           16940993p

Freebase ID (P646):                      /m/0vzt9zc

Quora topic ID (P3417):                  Shareconomy-1

JSTOR topic ID (P3827):                  sharing-economy
```

Listing the taxonomy raises some questions:
```
sharing economy (Q2277143) •29
├──crowd funding (Q348303) •45 ×2 ↑
├──carpool (Q749649) •30
├──car sharing system (Q847201) •29 ×4 ↑
├──bicycle-sharing system (Q1358919) •29 ×86 ↑↑↑
│  ├──bicycle-sharing system (Q17332642) •1
│  └──dockless bicycle sharing system (Q42556547) ×5
├──Flight sharing (Q18207130) •3
└──Rideshare (Q19698372) •3
```

I'm not convinced that systems like car sharing or crowdfunding are subclasses of the sharing economy, more that each could be considered a "part of" or "example of" it, so there is probably some room for improvement in this structure. And of course many other types of systems exist that contribute to a sharing economy. I've not yet found an ideal way to capture loose associations such as this.

Sometimes item labels start with capital letters, which for general classes should be lowercase, so that can be adjusted thus (replacing `<wd-id>` with a proper ID):
```
wd set-label <wd-id> en "$(wd label <wd-id> | tr '[:upper:]' '[:lower:]')"
```

There are lots more possibilities, I will update this post with more tips in future.

Many thanks to [maxlath](http://maxlath.eu/) and [nichtich](http://jakoblog.de/) for all their great work on this tools.
