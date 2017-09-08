---
layout: docs
title: Data Ingestion
description: Guide to Data Ingestion
group: getting-started
toc: true
---

## To aggregate your data from different sources
Microshare.io is here to help you aggregate and use your data from several sources, especially IoT platforms.  
Below are several way to move your data as [microshares™](../microshares-guide) in the data lake.  

## Upload data manually
Manual upload if the most basic way of loading data from your own database, or from a open data project.
To do so, send your data as the body of a [POST /share call](../api-overview#post-share).  
It will then be available to use from the data lake with [GET /share calls](../api-overview#get-share)

## Set up a websocket Robot
Some IoT platforms act as websocket servers and allow websocket clients to listen and pull data live.  
[Orange Live Objects](https://liveobjects.orange-business.com/), [The Things Network](https://console.thethingsnetwork.org/), or a Sagemcom private gateway support it.  
In Microshare.io, you can setup a websocket client Robot that takes care of writing your data as a microshare as soon as it is available.  
There is no UI to configure your own yet, but here is the WS client configuration we've gone with:
{% highlight java %}
{
  // A friendly name for the Robot.
  id = "My_WS_robot"
  // This microshare token assigns ownership of the created records.
  token = "My_MS_token"
  // The recType the incoming data will be stored under.
  recType = "io.sage.device.packed"
  // A tag to apply to the stored record.
  dType = "My_device"
  // The URI to the websocket server
  // If the WS service takes authorization as a query parameter, add it to the end of the URL.
  uri = "ws://my.websocket.uri?Authorization=Basic+My_WS_token"
  // if the service takes authorization as a header use below.
  authHeader = "Basic My_WS_header"
}
{% endhighlight %}

## Set up a scheduled Robot to pull data
Alternatively, some platform offer RESTful APIs to request for the data they store, such as [Orange Live Objects](https://liveobjects.orange-business.com/), [Bouygues Telecom Objenious](https://spot.objenious.com/login), [Sierra AirVantage](https://airvantage.net/#offers), or [Cumulocity](https://www.cumulocity.com/).  
In that case you can setup a [scheduled Robot](../robot-guide/#triggered-vs-scheduled) to perform GET calls to your IoT platform periodically.  
You are at liberty to setup your Robot script the way you want, to decide when and what to store as a microshare from that data.
Below is a sample code for a simple store all scenario.

{% highlight js %}
  //TODO Robot sample GET and write
{% endhighlight %}

## Set up your platform to post the data
For [Actility ThingsPark](https://partners.thingpark.com/en/dashboard) or a Kerlink private gateway.
Some platforms an be configured to POST data. Configure them to do a POST /share/:recType call.  

## What's next?
Once your data is loaded in the data lake, you'll want to get it ready to be used in Dashboards and Applications. Build your multisteps worflow with a [Pipeline Workflow](../pipeline-workflow) to parse, transform and format your data automatically.  