Challenge 01:
=============

### Bid Price: $100.0 CAD

### HackOn(Data) Points: 25

Having a list of networks and channels:

`channels_networks.csv`
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

The data cleansing task should be performed on the content of `channels_networks.csv`:

Notes: 
- The relation between Network to Channel is one to many. (e.g. There are many channels under FOX network)
- Network is not always provided, ignore if it's not there
- There are typos such as `blomberg` instead of `bloomberg`, inconsistent acronyms and naming conventions that need to be recognized
- Examples of inconsistency in acronyms:
  - (`HDTV` == `HD` == `hd` == `high-definition` == ...)
  - (`digital` == `dj` == ...)
  - (`west` == `(west)` == `ws` == ...)
  - ...

You could use `network_channels_master.json` as a guide to test your final result. This file is the list of channels with their network and meta information.

`network_channels_master.json`:
```
		"ChannelLineup": [{
			"Channel": {
				"ChannelNumber": 1,
				"ChannelId": 32046,
				"Network": "VOD",
				"NetworkCode": "VOD",
				"Format": "SD",
				"Streamable": false,
				"StreamableLocation": "None",
				"NetworkCategories": {
					"NetworkCategory": []
				},
				"CallSignDisplayLabel": "VODDM",
				"ChannelType": "VOD"
			},
			"Title": [{
				"TitleId": "SH005456030000",
				"Name": "On Demand",
				"SeriesId": "SH005456030000",
				"TmsId": "SH005456030000",
				"TitleType": "Series",
				"RunTime": 0,
				"OriginalDate": 1035676800000,
				"Advisory": {},
				"TVRating": "TVY",
				"Delivery": [{
					"TitleId": "SH005456030000",
					"DeliveryId": "32046-SH005456030000-1471615200000",
					"StartDate": 1471615200000,
					"EndDate": 1471629600000,
					"GuidePeriodMinutes": 60,
					"Channel": {
						"ChannelNumber": 1,
						"ChannelId": 32046,
						"Network": "Video On Demand",
						"NetworkCode": "VODDM",
						"Format": "SD",
						"Streamable": false,
						"StreamableLocation": "None",
						"NetworkCategories": {},
						"CallSignDisplayLabel": "VODDM"
					},
					"Duration": 14400,
					"Source": "Charter",
					"Transport": [{
						"TransportType": "QAM",
						"Format": "SD"
					}],
					"DeliveryType": "Linear",
					"TVRating": "TVY",
					"TVAdvisory": []
				}],
				"TitleCategories": {},
				"IsAvailableViaVod": false
			}, {
				"TitleId": "SH005456030000",
				"Name": "On Demand",
				"SeriesId": "SH005456030000",
				"TmsId": "SH005456030000",
				"TitleType": "Series",
				"RunTime": 0,
				"OriginalDate": 1035676800000,
				"Advisory": {},
				"TVRating": "TVY",
				"Delivery": [{
					"TitleId": "SH005456030000",
					"DeliveryId": "32046-SH005456030000-1471629600000",
					"StartDate": 1471629600000,
					"EndDate": 1471644000000,
					"GuidePeriodMinutes": 60,
					"Channel": {
						"ChannelNumber": 1,
						"ChannelId": 32046,
						"Network": "Video On Demand",
						"NetworkCode": "VODDM",
						"Format": "SD",
						"Streamable": false,
						"StreamableLocation": "None",
						"NetworkCategories": {},
						"CallSignDisplayLabel": "VODDM"
					},
					"Duration": 14400,
					"Source": "Charter",
					"Transport": [{
						"TransportType": "QAM",
						"Format": "SD"
					}],
					"DeliveryType": "Linear",
					"TVRating": "TVY",
					"TVAdvisory": []
				}],
				"TitleCategories": {},
				"IsAvailableViaVod": false
			}]
		},
		...
```



## Desired mapping dictionary:

```
channel_name_authoritative_mapping = {
  'FBN': {'primary_channel_name': 'Fox Business Network', 'network': 'fox', 'channel_id': '1234'},
  'Fox Business Net': {'primary_channel_name': 'Fox Business Network', 'network': 'fox', 'channel_id': '1234'},
  'FOX BUSINESS NETWORK': {'primary_channel_name': 'Fox Business Network', 'network': 'fox', 'channel_id': '1234'},
  ...
}

```

** Please note that `channel_id` must match the correct channel from `network_channels_master.json` key: `ChannelLineup.Channel.ChannelId`


For example:
```
channel_name_authoritative_mapping.get('Fox Business ntwk')
-> {'primary_channel_name': 'Fox Business Network', 'network': 'fox', 'channel_id': '123'}


channel_name_authoritative_mapping.get('FBN')
-> {'primary_channel_name': 'Fox Business Network', 'network': 'fox', 'channel_id': '123'}


channel_name_authoritative_mapping.get('blomberg')
-> {'primary_channel_name': 'Bloomberg', 'network': None, 'channel_id': '123'}


channel_name_authoritative_mapping.get('Bloomberg')
-> {'primary_channel_name': 'Bloomberg', 'network': None, 'channel_id': '123'}


```


## To Submit Your Solution:
1- Go to [TranQuant](http://tranquant.com)
2- Go to top menu `<Your E-mail>` > `My Data Publications`
3- Click on `Create new Data Source/Task` button
4- Create a new data source by filling out the form, you will be redirected to its edit page after creating it
4.1- You can set the category to `Open Data`
4.2- You should set the price to `0.00` and you can leave the `fields` and for `Agreement for Demand Data Usage`, `Tranquant Supplier Contract` you can just type `Open Data`
5- Install TQCLI according to [the instruction](https://github.com/Tranquant/tqcli)
6- Using the command under `Upload Dataset by TQCLI` in Data Source edit page, you can upload your solution dataset
7- If everything goes well you will see that the uploaded dataset will become available under the data source that you created on the TranQuant website
8- If you failed somewhere in this process. Please contact info@tranquant.com
