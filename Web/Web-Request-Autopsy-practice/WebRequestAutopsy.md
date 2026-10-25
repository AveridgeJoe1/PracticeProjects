# Web Review 01 : Web Request Autopsy 🔎

## Disclaimer : 
I am not an expert web developer so take all of this with a grain of salt. It's more just to go through the dev tools

## Task :

- Select 3 sites and 1 page "request autopsy" using browser developer tools, the timeline of the main document request, number of requests,total bytes, render blocking resources, and possible optimizations (probably picked using lighthouse), written as "phase" or "bottleneck"
- Include screenshots as evidence:
    - path > /{host}/{file}

## Purpose : 

- Review developer tool in browsers


--------------------
--------------------

### Site 1 : https://uga.edu/

 | Category     | Findings  |
 | ------------ | --------- |
 | Site and conditions | 10/25/26 , chrome , 4G throttling  , Network developer tool with disable cache ticked so, cold cache | 
 |Main document timeline |     • Queueing .67ms • Initial Connection/Stalled .65ms • Request .62 ms • Waiting for server response (TTFB) 166.32 ms • Content Download 3.94ms |
| Totals | 144 requests - 18.8 MB transferred – Load 7.65s -  LCP (in performance tab) 4.16s |
| Render-blocking (lighthouse) |  • /css/app.2150044f.css - 221.1 KiB - 400 ms • /js/app.535a9183.js - 98.4 KiB • /css/chunk-vendors.71d1adc2.css - 27.1 KiB • …js/dataprivacy-cookie.js(cdn.uga.edu) - 2.9 KiB - 370 ms • 2 CDNs -> • …font/bootstrap-icons.css(cdn.jsdelivr.net) 10.1 KiB - 370 ms • /css?family=…(fonts.googleapis.com) - 1.3 KiB - 370 ms | 
| Optimization |  Bottleneck is the video render and a few slow web fonts HTML is loaded in 172.2 ms but the first paint waits 1.1s and the LCP occurs at 5.3 s . The resource-blocking request identifies the css elements in uga.edu as well as third party web fonts used all with a load around 400ms. Marking fonts as optional may improve performance. The LCP breakdown in lighthouse identifies the div.video-buffering, which is the div where the mp4 video is loaded, as having a resource load delay of 3,300ms and load duration of 800ms. Exploring other compressed compatible file types may resolve this. As well as setting fetchpriority = high based on lighthouse suggestions |


