---
layout: post
title:      "Satoshi Gem"
date:       2018-10-19 13:21:20 -0400
permalink:  satoshi_gem
---


For my first project at Flatiron School we had to make a CLI gem. The gem should scrape information from the web, then get input form the user and then show more information. For my project I decided to scrape CoinMarketCap.com, and get the top 100 crypto currencies. Once you select a currency either by typing in the name directly or looking at the paginated list of coins and entering the appropriate number you are provided allot of up to date information on the coin. For Example USD price, BTC price, 24 volume, market cap, max supply, and circulating supply. 

At this point my project was done but I felt the need to take it a few steps further and make something that could possibly be useful. I then implemented a the option to add multiple coins to a type of ticker. That will constantly run until stopped in the terminal. The ticker runs every 5 seconds and scrapes the updated price from CoinMarketCap.com. It then compares that price to the previous one and changes the color to red black or green depending appropriately.  The most challenging part of this feature was learning that I had to start a new thread in order for the ticker to run while still be able to accept user input in order to stop the ticker. 

After completing this I thought it would be cool to be able to print out a graph in the terminal for any coin and found this good api for generating graphs as images cryptohistory.org. I then after much trial and error found a working gem to print images to the terminal called catpix. 

The most hardest problems to solve that I ran into while making this gem where figuring out how to correctly install rmagic in order to get catpix to work. Also I ran into an issue with the file path that I was saving the graph to when someone would install the gem from rubygems.org. I eventually learned that i needed to use __dir__ in order to get an absolute path the to gems file directory. 

