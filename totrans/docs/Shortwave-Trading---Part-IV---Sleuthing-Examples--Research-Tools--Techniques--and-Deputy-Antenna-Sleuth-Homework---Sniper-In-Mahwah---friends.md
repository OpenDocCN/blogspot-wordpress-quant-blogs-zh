<!--yml
category: 未分类
date: 2024-05-18 14:07:14
-->

# Shortwave Trading | Part IV | Sleuthing Examples, Research Tools, Techniques, and Deputy Antenna Sleuth Homework – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2018/07/16/shortwave-trading-part-iv-sleuthing-examples-research-tools-techniques-deputies-wanted/#0001-01-01](https://sniperinmahwah.wordpress.com/2018/07/16/shortwave-trading-part-iv-sleuthing-examples-research-tools-techniques-deputies-wanted/#0001-01-01)

*[Here is Bob Van Valzah’s last episode of the “Shortwave trading” series. Again, I’ll add a Part V about Europe when I’m back in my backyard, on Thursday. Meanwhile, I hope you’ll enjoy this last part from Bob – Alexandre]*

* * *

After my first few public posts about shortwave trading, I gradually realized that I’d inadvertently created a worldwide network of deputy antenna sleuths. This is the final post in the Shortwave Trading series since the terms of my forthcoming employment agreement will prohibit me from future public talk on the technology of trading. I want to leave behind details on some of the research tools and techniques I’ve used. This is how the sausage is made.

I’ll also leave a list of locations that may be worth watching. Some may be near you. Even if I can’t talk about what’s found in the future, maybe you can? The comments below might be a good place to document new findings until there’s a better place offered.

In addition, following sections will set out the criteria I’ve used to assess the confidence that a shortwave trading site has been found, give example FCC searches, list links to web-based research tools I’ve found useful, give some tips on research techniques, and acknowledge the many people behind the scenes who’ve contributed to this work.

> Two quick asides: [Video from my shortwave trading presentation](https://stacresearch.com/STAC-Summit-13-Jun-2018-shortwave-trading) at the [New York STAC Summit](https://stacresearch.com/spring2018NYC) is now available. It’s 31 minutes, including the Q&A at the end. Also, I recorded a [podcast episode on shortwave trading](https://itunes.apple.com/us/podcast/the-technology-evangelist/id1253336133?mt=2#). Try these if you’d rather watch or listen than read. Thanks to Peter Lankford at STAC for the video and to Scott Schweitzer at Solarflare for the podcast.[![VideoFrameGrab2](img/4b75aa996cf01234737cc602e1c08d3f.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/07/videoframegrab2.png)

### Plausibility Criteria

If you find something that looks like a shortwave trading site, how confident can you be that you’ve found the real thing and not a landing beacon for body-snatching space aliens? Since a shortwave trading site exists to link a local market to a remote market, I can think of two things that set a minimum bar for plausibility:

1.  Visual evidence of a shortwave antenna with a heading toward a remote market. Previous posts in this series have shown many shortwave antennas you can use as models of what to expect. Examples have included headings around 50º from Chicago which cover Europe.
2.  A path for connectivity to a local market. Visual evidence of this can be a microwave dish pointed in the direction of a local market.

I suppose that the best way to reach certainty that you’ve found a shortwave trading site would be for the owner of the site to publicly admit that it’s theirs, and that they’re using it for shortwave trading. That’s not going to happen, but there are still many scraps of circumstantial evidence that can add up.

*   Government licenses allowing shortwave transmission from the site.
*   Government licenses allowing microwave links between the site and a local market.

The credibility of your conclusions goes up if you can find government records that tie a site back to a trading company. Trading companies generally create shell companies to hold their shortwave trading assets. Look for:

*   Radio license ownership
*   Tower ownership (see FCC ASR database in Links below)
*   Zoning changes
*   Construction permits
*   Property sale records
*   Property tax records

Note that FCC licenses will have contact information. This is often a telecommunications lawyer with an office in Washington DC who prepared the license application, and also created the shell company to hold the license. One lawyer or one law firm may work on behalf of many clients, so consider any correlations circumstantial, but suggestive.

## FCC Search Examples

It’s tough to beat government records for adding credibility to your findings. Finding FCC licenses to transmit both shortwave and microwave from the same location is a great goal. There are many ways to search FCC databases, but I’ll give two examples searches for shortwave licenses. Once you have the coordinates where a shortwave license allows transmitting, I’ll show how to do a microwave search around those coordinates.

### FCC Shortwave License Search by City

Cell towers are by far the most common thing you’ll see, then maybe AM, FM, and TV transmitting antennas. But let’s assume you get lucky and spot something odd-looking in a city and want to check your hunch. I’ll use the city of West Chicago as an example.

You want to search for all experimental shortwave licenses in West Chicago, so you go to the [Experimental Licensing System Generic Search](https://apps.fcc.gov/oetcf/els/reports/GenericSearch.cfm) web site. Fill in the shortwave `Frequency Range` of 3 to 30 and select `MHz` from the unlabeled suffix drop-down menu. Fill in `Transmitter City` with West Chicago.

![Experimental City Search](img/97797b93161dddf3bc3413cd03390102.png)

Do **not** fill in the `Transmitter State` field or you’ll trigger a bug in the FCC website and get an error.

![FCC MAXLENGTH](img/b3bc0b29afac9100b6fadfa1def23e4d.png)

I’ve reported the behavior, been thanked, and told that it’s a known problem.

If your search returns any licenses, see the section below on reading FCC experimental license search results.

### FCC Shortwave License Search by Coordinates

My searching began with the question: “What experimental licenses allow shortwave transmitters within 100 miles of CME?” Here are the steps to do that query.

We need to have the coordinates for the center of our 100-mile search radius. I’ve heard that CME doesn’t officially reveal the location of their primary data center, but Google is happy to give you the answer directly in the search results so you don’t even have to click to see it.

![CME Datacenter Coordinates Google](img/f146d2da371ea155931f5b405f4fb685.png)

Google’s convenient answer brings up an important side point: there are several different geographic coordinate systems in use and it is sometimes necessary to [convert between](https://en.wikipedia.org/wiki/Geographic_coordinate_conversion) them. The query result above shows results in decimal degrees, but the FCC searches require degrees, minutes, and seconds. Instead of converting, it’s sometimes easier to find my target in Google Earth and then read degrees, minutes, and seconds from the display.

![CME Coordinates](img/8440a1fc1accd400bed77d467bb3e9eb.png)

Start with the [FCC Site / Frequency Query](https://fjallfoss.fcc.gov/General_Menu_Reports/engineering_search.cfm?service_select=Select&accessible=NO&state_select=&begin_freq=&begin_freq_type=M&end_freq=&end_freq_type=M&polar=B&radio_ch0=P&lat_ddd=&lat_ddd_cfforminteger=Latitude+degrees+must+be+numeric.&lat_mm=&lat_mm_cfforminteger=Latitude+minutes+must+be+numeric.&lat_ss=&lat_ss_cfformnumeric=Latitude+Seconds+must+be+numeric.&ns_radio_ch1=N&lon_ddd=&lon_ddd_cfforminteger=Longitude+degrees+must+be+numeric.&lon_mm=&lon_mm_cfforminteger=Longitude+minutes+must+be+numeric.&lon_ss=&lon_SS_cfformnumeric=Longitude+seconds+must+be+numeric.&ew_radio_ch1=W&radius=&Radius_cfformnumeric=Radius+must+be+numeric.&distance_type=&lat_ddd2=&lat_mm2=&lat_ss2=&ns_radio_ch2=&lon_ddd2=&lon_mm2=&lon_ss2=&ew_radio_ch2=&soundex_select=&begin_grant_date=&end_grant_date=&begin_expiration_date=&end_expiration_date=&sortstring=%2C+lic_name%2C+file_num&limit_select=4) page and set `Service Selection` to `Specific Services Only` and check the box for `Experimental Database`.

![Site:Freq Service](img/10a95c6ca0c52b1fac395d7509a86e51.png)

Set `Frequency` section `Begin` and `End` fields to 3 MHz and 30 MHz, respectively, to limit the search to shortwave frequencies.

![Site:Freq Freq](img/c1d41699e51b0dd77baabbcda249e87d.png)

In the `Location Search Method` section, click the `Point Radius` radio button.

![Site:Freq Location Search Method](img/9be56b181ac1b2a0d58737c3bafab0a5.png)

Now enter the coordinates for the center of your search and your search radius:

![Site:Freq Point Radius](img/62e7e840c1f3bc684caeb33c7846caf9.png)

Hit `Submit Query` and you should see several rows of output. I’ll just highlight the one for West Chicago. From this, you can get the coordinates needed for a microwave search.

![Site:Freq Search Result](img/593dcc583316c43c335ed02293e57e66.png)

You can also click on the `Callsign` link to query for all licenses for a station. Interpretation of the results is described in the next section.

### Reading FCC Experimental License Search Results

The experimental license query results I see for West Chicago look like this:

![West Chicago Experimenal Results](img/8a538433a4b059f7b7e8795c4545adb1.png)

As in this case, it’s common to see a list of expired and renewed licenses. It’s also common to see licenses updated long before they expire; these are experimental licenses after all. There may be no difference between the `Initial` and `Current` links in the left column, but if changes are made over the lifetime of the license, they’ll show up as a change there.

A granted license will be shown on FCC form 442\. See the form by following the `Current` link in the `View Form` column. It’s sometimes insightful to compare the changes relative to expired licenses to understand trends.

Note that your browser and the FCC’s web site may conspire to open FCC form 442 in a new tab or new window, leaving the search results still to be seen. Clicking on other form 442 links in the search results may just update the tab or window that was displaying earlier form 442 results, overwriting them.

An interesting part of the form is the `Manufacturer` section listing the transmitting equipment used. This often includes the transmitter, modem, or SDR, power amplifier, and antenna.

![442 Manufacturer](img/c8191ef991fd99bbbd27ebbb46c58b07.png)

The form ends with a `Station Location` section, with subsections for each site where the licensee may transmit. The GPS coordinates for latitude and longitude should get you very close to the antenna location. But be aware that the street address and city may be approximate. Some of the sites I’ve visited are far enough out that they may not be part of an incorporated city. The address used on mapping apps seem to go by the city handing postal mail delivery for the area, which might be different from how the FCC sees the address.

![442 Location](img/a707e4a0a7a708db1ea9dfb2aa8a50c3.png)

Applicants sometimes request redaction of the antenna heading (degrees from True North above). But when they do, you just have to visit the site and stand under an imaginary line in the sky pointing in the direction of the shortwave antenna heading. Walk away from the antenna site along this line, pausing every 500 feet or so. Make sure you’re still on the heading line and take a picture of the antenna with your cell phone. Back at home, get the GPS coordinates of the pictures and plot them with GoogleEarth to get the heading line. It only takes a few points to establish a line.

### FCC Microwave License Search by Coordinates

Microwave links use well-established technology so there’s no need to experiment. Such licenses are part of the [Universal License System (ULS) online database](http://wireless2.fcc.gov/UlsApp/UlsSearch/searchLicense.jsp). If we have the station location coordinates from a shortwave experimental license, we can use those to look up associated microwave licenses nearby. I haven’t found an easy way to do geographic ULS searches, so this is a multi-step process. Start by following the `Site Based` link.

![ULS Site Based Link](img/e059dd1297692c8cea0e8591564a624c.png)

Microwave licenses of interest will come from the business pool, so select `MG` from the `Site Based` section and the `Radio Service Code` scrolling list.

![ULS Select MG](img/8b138a819ad9d460a74ff26161187593.png)

Then make sure you hit the `GeoSearch` button, **not** the `Search` button.

![ULS GeoSearch Button](img/b2bd9d20c9bf84458d09be9324d4b02d.png)

Click the `Coordinates` radio button and fill in `Latitude`, `Longitude`, and `Radius`. You can use a small radius if you’re confident in the accuracy of the coordinates you have, otherwise you may have to increase it to get a hit. Click the `Search` button.

![ULS Coordinates](img/6cdc5be7eee21ee96bed8a2bdc37568d.png)

The search results I see look like this:

![ULS Microwave Search Result](img/e93fdb9cc49ad87bc1cbb23556b5656e.png)

This shows two microwave licenses, one for the microwave transmitter near CME and the other for the microwave transmitter at West Chicago. Click on either license to bring up the main page.

![ULS Microwave Main Tab](img/197d249d887a5e9d7cde27f14f30a4c1.png)

Now click on the `Map` tab to see the location of the other end of the link:

![ULS Microwave Map Tab.png](img/7dae2384b7e529f5239fef31d7cafb4f.png)

Note that sometimes microwave searches find no license when it sure seems like they should. I know one reason is that sometimes higher frequencies are used instead (“millimeter wave”). The FCC doesn’t require point-to-point licenses at these frequencies. However, the rules as I understand them still require that point-to-point links be registered in a frequency coordination database (see Micronet database in Links below). Check there before giving up.

But even with that, I still see links in the air that I can’t find in a database anywhere, so I think I’m still missing something. I’d love to hear about it in the comments below if any readers know how to do a more thorough search.

### Links to Research Tools

*   **[FCC Experimental License Site or Location Search](https://fjallfoss.fcc.gov/General_Menu_Reports/engineering_search.cfm?service_select=X%2521&state_select=&begin_freq=&begin_freq_type=M&end_freq=&end_freq_type=M&polar=B&radio_ch0=P&lat_ddd=&lat_mm=&lat_ss=&ns_radio_ch1=N&lon_ddd=&lon_mm=&lon_ss=&ew_radio_ch1=W&radius=&distance_type=&lat_ddd2=&lat_mm2=&lat_ss2=&ns_radio_ch2=&lon_ddd2=&lon_mm2=&lon_ss2=&ew_radio_ch2=&ACCESSIBLE=NO&soundex_select=&begin_grant_date=&end_grant_date=&begin_expiration_date=&end_expiration_date=&sortstring=%2C+lic_name%2C+file_num&limit_select=4):** All the confirmed shortwave trading sites I found were in this database. Use this link to search for licenses with transmitter sites within a radius of GPS coordinates.
*   **[FCC Experimental License Generic Search](https://apps.fcc.gov/oetcf/els/reports/GenericSearch.cfm):** Same data as the link above, but just the search criteria that aren’t location focused. There is some overlap in criteria allowed with the above link.
*   **[FCC Universal License Search](http://wireless2.fcc.gov/UlsApp/UlsSearch/searchLicense.jsp):** Non-experimental licenses, including those used for microwave links.
*   **[FCC Antenna Structure Registration (ASR) Search](http://wireless2.fcc.gov/UlsApp/AsrSearch/asrRegistrationSearch.jsp):** Search the database of towers and other places you’d ever want to put an antenna. See FCCInfo below.
*   **[FCC FRN Search](https://apps.fcc.gov/coresWeb/simpleSearch.do):** Every business or individual that interacts with the FCC must have an FCC Registration Number (FRN). Licenses and antenna site ownership are tied back to FRN. Companies desiring secrecy will create shell companies to register with the FCC.
*   **[FCC Application Search](http://wireless2.fcc.gov/UlsApp/ApplicationSearch/searchAppl.jsp):** Applications are sent to the FCC to request a license. There may be interesting nuggets of history or things that don’t make it into the issued license. One example is an application to transfer control of a license from one company to another.
*   **[Micronet Millimeter Link Database Query](http://www.micronetcommunications.com/LinkRegistration/Query.aspx):** May be able to find links that don’t appear in FCC ULS searches.
*   **[Google Earth Pro](https://www.google.com/earth/desktop/):** Indispensable. The mobile versions may be ok for quick checks in the field, but I found I really needed the power of the desktop version. I looked for a way to share placemarks between desktops or between desktop and mobile, but no success. So I ended up having to do all my research on one desktop, but see next bullet.
*   **[Google Earth Web](https://earth.google.com/web):** Some of my challenges with Google Earth might’ve been eased if my browser of choice was Chrome or Firefox. Being willing to sign into Google everywhere probably would’ve helped sharing too.
*   **[Google Maps](https://www.google.com/maps/):** Great for planning driving and biking routes to visit antenna sites.
*   **[Google Street View](https://support.google.com/maps/answer/3093484?co=GENIE.Platform%3DDesktop&hl=en):** I didn’t know “Pegman” had a name until I read the linked support document.
*   **Apple Maps:** Uses a different database than Google. It sometimes helps to have a second opinion. Aerial imagery freshness is sometimes better than Google, sometimes worse. Don’t forget to try satellite mode and “3D.”
*   **[FCCInfo on Google Earth](http://www.fccinfo.com/fccinfo_google_earth.php):** This is an amazing little tool that you download once and install into Google Earth on your desktop. It’s focused on AM, FM, and TV stations, but there’s no need to check these boxes unless you want to know where your local broadcast stations have their antennas. In the `Places` panel, click `FCCInfo`. When that expands, click `ASR Towers`. This will display red vertical lines reflecting all registered ASR towers. Towers over 200 feet must be registered, as must those close to an airport runway. This includes many of the towers I found to be used for shortwave trading and microwave links.
*   **[GeoHack](https://tools.wmflabs.org/geohack/):** A nice abstraction layer for mapping, satellite imagery, and more. Enter GPS coordinates and get a page of links to various web-based services for maps and imagery of the site. For example, here’s the [page for the West Chicago Tower location](https://tools.wmflabs.org/geohack/geohack.php?params=41_53_54_N_88_13_14_w). Note the lack of western-hemisphere bias: longitude defaults to east.
*   **[Compare Licenses](https://www.copyscape.com/compare.php):** You can sometimes draw interesting conclusions by comparing how experimental licenses change over time. This is a tedious process if done manually, but there are many web sites that will take two URLs for two different experimental licenses from the FCC database and highlight just the differences.
*   **[Emission Designator Reference](http://www.swld.com.au/pages/emissions.pdf):** Experimental licenses will give “emission designators” that compactly describe how information is encoded for transmission (i.e. how the radio carrier is modulated). This link explains the compact encoding used by the FCC.

### Research Techniques

*   **Do Field Work Respectfully:** Please be respectful of nature and the property and wishes of others. Avoid trespassing *[I confirm, that’s important: once I entered a private tower/property and the big HFT that owns the tower called the FBI – true story, Alexandre]*.
*   **Bookmarks:** These posts contain well over 100 links that I curated from probably more than 1,000 web pages reviewed in pulling this material together. I had to set aside my old bad habits of piling up browser windows, each with countless tabs. Given many simultaneous lines of investigation and countless tangents, the old way just didn’t scale. Find a way to organize bookmarks and sync them across devices. Maybe [Pinboard](https://pinboard.in/) if you don’t like the services provided by your browser?
*   **Screenshots:** Find a convenient way of taking screenshots and annotating them. I use the key combination `Command-Control-Shift-4` on my Mac to begin selecting an interesting screenshot area. I paste that into `Preview` and annotate it there. I think 10.14 has something even better in the offing.
*   **Who Owns That Antenna?** I want to avoid angering potential employers who’ve gone to a lot of effort to obscure ownership of their shortwave trading assets, so I haven’t talked much about ownership. Yet reporters have combed through public records and figured it out in [some](https://spectrum.ieee.org/tech-talk/telecom/wireless/wall-street-tries-shortwave-radio-to-make-highfrequency-trades-across-the-atlantic) [cases](https://www.bloomberg.com/news/articles/2018-06-18/hft-traders-dust-off-19th-century-tool-in-search-of-market-edge). They don’t tell you how they did it, but [Matt Hurd has shown how he connected the dots](https://meanderful.blogspot.com/2018/06/shortwave-trading-who-is-that-in-bob.html) on his excellent [Meanderful blog](https://meanderful.blogspot.com/).
*   **Latest Imagery:** Watch out for the Google Earth checkbox in the lower-left hand corner under `Layers` for `3D Buildings`. It does make the buildings look better in some places, but it can have the side effect of hiding more recent imagery that doesn’t have the 3D info. I recommend running without `3D Buildings` checked.

### Deputy Antenna Sleuth Homework

If you’re intrigued by shortwave trading, I can think of a few things you may be able to do to help us all learn more. Please add to the comments below if you see anything interesting.

*   **Observe Changes Near You:** If you live near one of the known shortwave trading sites, please keep an eye on the antennas as you drive by.
*   **Repeat FCC Geographic Searches:** Every few months, it’s probably a good idea to repeat searches around trading market data centers and transoceanic cable landing stations. As I’ve shown in Part III, things were still rapidly changing as of mid 2018.
*   **Watch Alpine, New Jersey:** I mentioned in Part III that an unusual kind of [shortwave broadcast license](https://ecfsapi.fcc.gov/file/104112444521024/TURMS%20TECH%20-%20FCC%20Form309%2004-11-2017.pdf) had been granted for an [antenna site in Alpine, New Jersey](https://tools.wmflabs.org/geohack/geohack.php?params=40_57_40.4_N_73_55_24_w). Construction had been approved for nearly a year with no activity when I checked it. A drone would be a good way to check the site. The local police knew I was looking around because I left my car parked where it could be seen from the main road.[![](img/511090187e3e6868d337f84bc1d35bfc.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2018/07/capture-d_ecc81cran-2018-07-16-acc80-20-51-39.png)

    The Alpine towers seen by Google Earth, 3D option on

*   **Watch Anchorage, Alaska:** An [experimental license](https://apps.fcc.gov/oetcf/els/reports/442_Print.cfm?mode=current&application_seq=78952&license_seq=79672) has been approved for transmitting from Anchorage, Alaska. The same license covers transmitting from Aurora, Illinois and Secaucus, New Jersey. The [Anchorage antenna site](https://tools.wmflabs.org/geohack/geohack.php?params=61_6_13_N_149_40_18_w) would be very near the shortest path between CME and Tokyo. The shortwave antenna heading would be pointing at Tokyo. That’s a pretty good pile of circumstantial evidence that shortwave trading is planned for the site. I couldn’t find pictures of anything that had been built there when I looked around with Google Street View.
*   **Watch Orangeburg, New York**: [The license](https://apps.fcc.gov/oetcf/els/reports/442_Print.cfm?mode=current&application_seq=83686&license_seq=84556) for one of the sites built near CME also allow transmission from an [antenna site not far from Mahwah](https://tools.wmflabs.org/geohack/geohack.php?params=41_1_53_N_73_58_36_w), just over the border into New York. This is likely where they’ll build if they expand to the east coast.
*   **Watch Seattle, Washington**: [The license](https://apps.fcc.gov/oetcf/els/reports/442_Print.cfm?mode=current&application_seq=84316&license_seq=85209) for another site built near CME also allows transmission from an [antenna site](https://tools.wmflabs.org/geohack/geohack.php?params=47_36_55_N_122_18_33_w) not far from the landing station for the [PC-1 cable](http://www.pc1.com) connecting to Japan. But note that license contains a typo on the longitude for the antenna site–it should be 122 degrees west, not 112 degrees west.
*   **Watch Wesley Hills, New York**: The license covering Seattle also allows transmission from [an antenna site](https://tools.wmflabs.org/geohack/geohack.php?params=41_9_38_N_74_5_19_w) in Wesley Hills, New York. This is the one with the camouflaged cell tower that I mentioned in Part III. This is my bet for where they’ll expand on the east coast.
*   **Watch Glendale Heights, Illinois**: [This antenna site](https://tools.wmflabs.org/geohack/geohack.php?params=41_55_49_N_88_5_14_w) is right on the shortest path between CME and Europe. It could have a latency advantage when transmitting, compared to the more rural sites chosen to minimize receiving noise. The existing tower had two cellular carriers and no shortwave when I visited on April 11, 2018.

### Acknowledgements

Primary thanks go to Alexandre Laumonier (a.k.a. Sniper In Mahwah) who’s pioneering work on the *HFT In My Backyard* series of posts inspired me to undertake this work.

My public posts about shortwave trading brought out not only deputy antenna sleuths, but also advisors who can’t talk publicly. Thanks to all the insight they provided on the QT.

Thanks to all who’ve commented on previous posts. Please comment here if you find anything interesting or develop any other research techniques.

* * *

![](img/4259dd9f21b8587e01911dd83ab44a89.png)

One of the shortwave sites visited by French sound artists working on a project about the “sounds” of high-frequency trading. © Jean-Philippe Renoult & Dinah