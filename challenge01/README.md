Challenge 01:
=============

Having a list of networks and channels: [networks_channels.csv](networks_channels.csv)

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

1- You need to unify the channel names, in some instances you can find duplicates for the same channel such as `('Fox Business Net', 'Fox Business Network') `
or in some instances you can find their acronyms being used instead of full name such as `('FOX BUSINESS NETWORK HD', 'FBN-HD')`

2- You need to find all channels that belong to a network and organize them as a dictionary where the keys are networks and channels are the values.

## At the end we need the following dictionaries as your final result:

```
channel_name_authoritative_mapping = {
  'FBN': 'Fox Business Network',
  'Fox Business Net': 'Fox Business Network',
  'FOX BUSINESS NETWORK': 'Fox Business Network',
  ...
}

networks_channels = {
  'FOX': ['Fox News Channel HDTV', 'Fox Business Network', ...],
  ...
}
```
