HackOn(Data) Challenge 01: TV Network Channels List - Data Cleansing Task
=============
Sponsored by `Audience Partners Canada`


[Data Resources on TranQuant](http://tranquant.com/datasource-detail/cdc72da2-096a-4733-a0a1-4443ab88c6bc)

### Prize: $100.0 CAD

### HackOn(Data) Points: 25

### Deadline: August 27th, 23:00 pm - No Late Submissions will be accepted

The data cleansing task should be performed on the content of `channels_networks.csv`:

`channels_networks.csv` has a list of networks and channels:

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


## Example:

On `networks_channels.csv` file you can find these records:
```
'network', 'channel'
'','Fox Business Net'
'','FOX BUSINESS NETWORK'
'','Fox Business News'
'','Fox Business Ntwk'
'','FBN-SD'
...
```

Now if you search through `network_channels_master.json` you will find Channel records for `Fox Business`.

You can find `Fox Business` as the network name with Channel ID `58649`

```
"Channel": {
    "ChannelNumber": 95,

    "ChannelId": 58649,

    "Network": "Fox Business",

    "NetworkCode": "FBN",
    "NetworkLogoUri": [{
        "ImageUri": "http://tmsimg.video.cdn.charter.com/h3/NowShowing/58649/s58649_h3_aa.png",
        "ImageType": "For Light Background",
        "ReferenceType": "Network",
        "Width": 360,
        "Height": 270,
        "DefaultImage": true
    }],
    "Format": "SD",
    "Streamable": false,
    "StreamableLocation": "None",
    "NetworkCategories": {
        "NetworkCategory": ["News & Weather"]
    },
    "VodFolderId": "44da38afd3816562f3dc7f4ddaf4d3d7",
    "SDHDPair": 58718,
    "CallSignDisplayLabel": "FBN"
}
```

Now you have the ChannelId for all those 4 records with similar name that we saw on `networks_channels.csv`. The desired records in your final dataset should look like:

```
channel_name_authoritative_mapping = {
 'Fox Business Net': {'primary_channel_name': 'Fox Business', 'network': '', 'channel_id': '58649'},
 'FOX BUSINESS NETWORK': {'primary_channel_name': 'Fox Business', 'network': '', 'channel_id': '58649'},
 'Fox Business News': {'primary_channel_name': 'Fox Business', 'network': '', 'channel_id': '58649'},
 'Fox Business Ntwk': {'primary_channel_name': 'Fox Business', 'network': '', 'channel_id': '58649'},
 'FBN-SD': {'primary_channel_name': 'Fox Business', 'network': '', 'channel_id': '58649'},
 ...
}
```

** Please note that `channel_id` in your solution must match the correct channel from `network_channels_master.json` on key: `ChannelLineup.Channel.ChannelId`


For example:
```
channel_name_authoritative_mapping.get('Fox Business ntwk')
-> {'primary_channel_name': 'Fox Business', 'network': '', 'channel_id': '58649'}


channel_name_authoritative_mapping.get('FBN-SD')
-> {'primary_channel_name': 'Fox Business', 'network': '', 'channel_id': '58649'}


```


## To Submit Your Solution:
1. Go to [TranQuant](http://tranquant.com)
2. Go to top menu `<Your E-mail>` > `My Data Publications`
3. Click on `Create new Data Source/Task` button
4. Create a new data source by filling out the form, use `RE: TV Network Channels List - Data Cleansing Task` as the title - you will be redirected to its edit page after creating it (You can set the category to `Open Data`, You should set the price to `0.00` and you can leave the `fields` and for `Agreement for Demand Data Usage`, `Tranquant Supplier Contract` you can just type `Open Data`)
5. Install TQCLI according to [the instruction](https://github.com/Tranquant/tqcli)
6. Using the command under `Upload Dataset by TQCLI` in Data Source edit page, you can upload your solution dataset
7. If everything goes well you will see that the uploaded dataset will become available under the data source that you created on the TranQuant website
8. Let us know about your solution by leaving a review on the original data task with a link to your data source and send us an email 
9. If you failed somewhere in this process. Please contact info@tranquant.com
