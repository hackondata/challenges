Challenge 01:
=============

Having a list of networks and channels: [networks_channels.csv](URL)

## Header: Network, Channel
```
"","Fox News Channel HDTV"
"","Showtime Showcase HDTV (West)"
"","HBO HDTV On Demand"
"","WHDH"
"","AMC"
"","Adult Alternative"
"","NHL/MLB 9"
"","Independent Film Channel"
"","Canal 22 HD"
"PBS","WAIQ"
"","VELOCITY"
"","Telemundo"
"","ENCR WEST"
"PBS","WNIT HDTV"
"ANTEN","WILX Antenna TV"
"MNT","Rockford's My Network TV HDTV"
"","SMITHSONIAN HD"
"","Disnet JR."
"","ST. Genevieve Info"
"","Tomahawk HS"
"TELMUN","KKCO 3 Telemundo"
"","MTV2 (West)"
"THIS","KPIC ThisTV"
"","TW DEPORTES-DI"
"","NICKELODEON-DI"
"","BOMERANG"
"","SDV EPIX"
"","SHOSH"
"","National Geographic Channel"
"","Encore Action (East)"
"","Fusion HD"
"","Liquidation in HD"
"ABC","WZZM"
"MNT","WTVZ"
```

Notes: 
- The relation between Network to Channel is one to many. (e.g. There are many channels under FOX network)
- Network is not always provided, ignore if it's not there
- There are typos such as `blomberg` instead of `bloomberg`, inconsistent acronyms and naming conventions that need to be recognized
- Examples of inconsistency in acronyms:
  - (`HDTV` == `HD` == `hd` == `high-definition` == ...)
  - (`digital` == `dj` == ...)
  - (`west` == `(west)` == `ws` == ...)
  - ...

You are going to create a mapping that allows looking up a consistent channel name.

## Desired mapping dictionary:

```
channel_name_authoritative_mapping = {
  'FBN': {'primary_channel_name': 'Fox Business Network', 'network': 'fox'},
  'Fox Business Net': {'primary_channel_name': 'Fox Business Network', 'network': 'fox'},
  'FOX BUSINESS NETWORK': {'primary_channel_name': 'Fox Business Network', 'network': 'fox'},
  ...
}

```


For example:
```
channel_name_authoritative_mapping.get('Fox Business ntwk')
-> {'primary_channel_name': 'Fox Business Network', 'network': 'fox'}


channel_name_authoritative_mapping.get('FBN')
-> {'primary_channel_name': 'Fox Business Network', 'network': 'fox'}


channel_name_authoritative_mapping.get('blomberg')
-> {'primary_channel_name': 'Bloomberg', 'network': None}


channel_name_authoritative_mapping.get('Bloomberg')
-> {'primary_channel_name': 'Bloomberg', 'network': None}


```
