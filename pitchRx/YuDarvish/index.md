Animating PITCHf/x Data (using pitchRx)
========================================================

A case study of Yu Darvish's deception factor
---------------------------------------------------

On April 2nd, 2013 Yu Darvish [flirted with pitching perfection](http://sports.yahoo.com/news/yu-darvish-loses-perfect-game-030913556--mlb.html). To demonstrate his ability to deceive batters with a consistent delivery over different pitch types, [redditor DShep created this gif](http://www.reddit.com/r/baseball/comments/1d2z6d/all_of_darvishs_primary_pitches_at_once/), which layers video of five different pitches thrown by Darvish on April 24th:

<img class="decoded" src="http://i.minus.com/i3SXAH4AAxtWS.gif" alt="http://i.minus.com/i3SXAH4AAxtWS.gif"></img>

Cool, huh? Well, I will show you how to 'recreate' a similar 'gif' with publicly available PITCHf/x data using the [pitchRx](http://cran.r-project.org/web/packages/pitchRx/) [R](http://cran.r-project.org) package. First, we collect all the pitches thrown by Darvish to Albert Pujols on April 24th:


```r
library(pitchRx)
library(plyr)
dat <- scrapeFX(start = "2013-04-24", end = "2013-04-24")
atbats <- subset(dat$atbat, pitcher_name == "Yu Darvish" & batter_name == "Albert Pujols")
pitches <- plyr::join(atbats, dat$pitch, by = c("num", "url"), type = "inner")
```


Then we animate these pitches using `animateFX`. 





```r
animateFX(pitches)
```

<embed width="504" height="504" name="plugin" src="figure/ani.swf" type="application/x-shockwave-flash">


According to the PITCHf/x data, Darvish had quite different release points (especially for his slider). Furthermore, Darvish didn't even throw a curveball to Pujols. If you look closer at the original gif, you can actually see a different batter (than Pujols) in the batter's box (look for a white bat). 

I think it would be awesome to have a similar tool in [pitchRx](http://cran.r-project.org/web/packages/pitchRx/) for creating 'gifs' with actual video. If anybody has ideas on how we can connect PITCHf/x data with actual video, leave a comment or mention me on twitter [@cpsievert](http://twitter.com/cpsievert).

If you're still reading, you may be wondering, how can I take these animations and embed them on my own web page/blog? To create this page - and [many](http://cpsievert.github.io/pitchRx/demo/) [others](http://cpsievert.github.io/pitchRx/rgl1), I use [knitr](http://yihui.name/knitr/). I've written this specific post in [Markdown and published via RStudio](http://www.rstudio.com/ide/docs/authoring/using_markdown). Here is the source code to the page:

