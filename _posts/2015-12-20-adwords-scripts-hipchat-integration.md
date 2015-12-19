---
layout: post
title: AdWords Scripts and Hipchat integration
description: "An implementation that reports the performance of campaigns in your account"
categories: adwords
tags: [javascript, hipchat, integration, adwords]
---
This script loops over 10 campaigns (no order specified) and sends those stats for each of them for "LAST_7_DAYS". If you want those stats for any other window, change it in line 2 by changing the value against LOOKUP_WINDOW. The options are [available here](https://developers.google.com/adwords/scripts/docs/reference/adwordsapp/adwordsapp_campaign#getStatsFor_1).

You have to provide the API url of the hipchat room that receives the messages. Login to hipchat.com web interface as an Admin. Go to Integrations of the room, click "New". Click the Create button under the "Build Your Own!", and name the integration to something you remember. Click Configure on the integration, and note the field "Send messages to this room by posting to this URL". The url will look like: `https://api.hipchat.com/v2/room/(room-id)/notification?auth_token=(token)`. That's the API url. Please paste in line 1 against ROOM_API_ENDPOINT.

Let me know if you face any issues. If you want different stats or pick campaigns in some order or something else, let me know and I'll change it.

{% highlight javascript %}
// Author: Manu Ganji (http://manuganji.com)
// Credits for the base version: Cristian's Blog (http://csimms.botonomy.com/2015/10/how-to-integrate-adwords-with-hipchat.html)

var ROOM_API_ENDPOINT = 'API url';
var LOOKUP_WINDOW = 'LAST_7_DAYS';// find other options at the link below
// https://developers.google.com/adwords/scripts/docs/reference/adwordsapp/adwordsapp_campaign#getStatsFor_1

// Make a small report and send it.
function main() {
  // Get enabled campaigns.
  var campaignIterator = AdWordsApp.campaigns()
      .withCondition("Status = ENABLED")
      .withLimit(10)
      .get();

  Logger.log('Active campaigns');
  while (campaignIterator.hasNext()) {
    var campaign = campaignIterator.next();
    var stats = campaign.getStatsFor(LOOKUP_WINDOW);
    Logger.log(campaign.getName() + ':\n' +
        stats.getClicks() + ' clicks\n' +
        stats.getImpressions() + ' impressions\n' +
        100*stats.getCtr() + ' click thru rate\n' +
        stats.getAverageCpc() + ' avg cpc\n' +
        stats.getCost() + ' cost\n'        
    );
    var percent = stats.getImpressions() ?
        Utilities.formatString('%1.3f', 100*(stats.getClicks() / stats.getImpressions()))
        : 'UNKNOWN';
    var currency = AdWordsApp.currentAccount().getCurrencyCode();
    var accountName = AdWordsApp.currentAccount().getName();
    var text  = "Stats for "+ accountName + "\n";
    text += "for the daterange: "+ LOOKUP_WINDOW + "\n";
    text += campaign.getName() + ':\n  ' +
      stats.getClicks() + ' / ' + stats.getImpressions() + ' clicks (' + percent + '%)\n  ' + currency +
        stats.getAverageCpc() + ' avg cpc, total: '+ currency + stats.getCost();
    Logger.log(text);
    
    var hipchat_msg = {
      'message': text,
      'message_format':'text',
      'notify':true
    };
    
    var params = {
     "method" : "post",
     "payload" : JSON.stringify(hipchat_msg),
     "contentType": "application/json"
    };

    UrlFetchApp.fetch(ROOM_API_ENDPOINT, params);
  }
}
{% endhighlight %}
