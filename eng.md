# Performance Matters

> **A note from the editors:** In each installment, an author from the W3C will 
keep you informed on what we're up to—and how you can be a part of it. This 
column is from Jatinder Mann, Internet Explorer Program Manager and Editor in 
the W3C Web Performance Working Group. Jatinder would like to thank Working 
Group co-Chairs Arvind Jain and Jason Weber, and W3C's Philippe Le Hégaret for 
their input on the piece.

While a decade ago it may have been okay to go brew a pot of coffee while the
computer was loading, today we all expect our software and devices to be fast
and responsive. The same holds true for web performance. The load speed and
responsiveness of a web application play a critical role in our choice of which
applications we want to use. At the same time, how efficiently software runs
plays a critical role in device battery life. No one wants to be carrying around
a brick.

To build fast web applications, web developers need to be able to qualitatively
measure application performance, effectively use their hardware, and most
importantly, know which patterns to optimize and which to avoid.

We found that web developers haven’t had the right tools. Left on their own to
guess, web developers in many cases only emphasized JavaScript performance and
equated JavaScript performance with web performance.

However, web performance is truly a multi-dimensional problem. How quickly the
network can download resources, how efficiently the CPU can perform web runtime
operations, and the amount of available GPU memory all impact web performance.
Let’s take a closer look at an example I gave in a [Build][1] presentation
involving five real world travel booking web applications: Kayak, Expedia,
Priceline, Travelocity, and Orbitz. All of these sites have very similar
elements on the page. They all have logos, banner ads, interactive real time
flight data, etc. We would expect them all to have very similar performance
characteristics.

Figure 1 shows the metrics for each of these sites, anonymized here to avoid
poking at anyone. We can see that even though these travel sites have very
similar functions, they have all been designed very differently. Some have more
bytes coming down the wire, others have more JavaScript.

<table>
<tr><th></th><th>Total Size (k)</th><th>Number of Elements</th><th>CSS Rules</th><th>Image Files</th><th>Script Lines</th></tr>
<tr><td>Site #1</td><td>3,697</td><td>1,504</td><td>1,392</td><td>41</td><td>77,768</td></tr>
<tr><td>Site #2</td><td>2,278</td><td>1,100</td><td>5,325</td><td>29</td><td>39,183</td></tr>
<tr><td>Site #3</td><td>1,061</td><td>2,673</td><td>1,105</td><td>66</td><td>12,643</td></tr>
<tr><td>Site #4</td><td>1,812</td><td>4,252</td><td>1,672</td><td>12</td><td>10,284</td></tr>
<tr><td>Site #5</td><td>1,372</td><td>900</td><td>3,902</td><td>6</td><td>38,269</td></tr>
</table>

Many developers would assume that the fastest site would be the one with the
least number of formatted lines of JavaScript, like Site #4, or the one with the
least bytes downloaded, like Site #3. However, that’s not the case. Site #5 is
actually the fastest, even though it has more JavaScript and bytes downloaded.
Figure 2 breaks down the amount of time each of these sites spent in the
different browser subsystems, subsystems all standards-based web browsers have.

![chart][Bar chart showing browser subsystem load times in milliseconds for five sites]

*Time spent in browser subsystems to load top five travel sites.*

There are really two points here. It’s not just about how to most efficiently
execute JavaScript, it’s about how all of the browser subsystems can most
effectively work together. Without the right tools, developers don’t really know
why their applications are slow and what to optimize.

Most web experts realized that there was a need for better interfaces to help
developers measure their applications and write faster code. More importantly,
there was a need for a forum to talk about performance problems that web
developers faced and how to solve them.

At tech conferences, folks like Steve Souders and Arvind Jain from Google, Jason
Weber from Microsoft, Jason Sobel from Facebook, and others started discussing
performance-related issues, such as an accurate and interoperable way to measure
page navigation time. These conversations soon led to the establishment of a
working group in the W3C focused solely on performance. It was in the summer of
2010 that Jason Weber from Microsoft and Arvind Jain from Google were selected
to co-chair the newly minted W3C Web Performance Working Group, chartered to
identify and solve performance issues that developers encountered on the web.

Not everyone was certain all these competitors could work together. The first
comment on the IE Blog [post][2] announcing this working group, referring to the
Google and Microsoft co-chairing of the working group, was “I bet the Richter
scale could pick up the tension in that room.” Fast forward to 2013 (and
ignoring the fact that the Richter scale isn’t an actual instrument), and the
Web Performance Working Group can really be seen as an example of the ideal
working group. In just three years, Microsoft, Google, Mozilla, Intel,
DynaTrace, and others in this group have designed APIs to help developers
measure their web applications more accurately and precisely than ever before
([Navigation Timing][3], [Resource Timing][4], [User Timing][5], [Performance
Timeline][6],[ High Resolution Time][7]), and more efficiently schedule
activities in web applications ([requestAnimationFrame][8], [Page
Visibility][9], [Efficient Script Yielding][10]). Based on the conversations
from the [W3C Workshop on Web Performance][11], which this working group put
together to hear from 45 performance experts and web developers from 21
organizations, the working group is now actively working on six new
specifications to solve other performance problems: efficiently prioritizing the
download of resources ([Resource Priorities][12]), asynchronously transferring
data without blocking page unloads ([Beacon][13]), getting detailed network
error and availability information ([Navigation Error Logging][14], [Resource
Error Logging][15]), marking links to be instantly loaded (Prerender),
standardizing on a performance metric format (HAR—HttpArchive), and improving
existing interfaces ([Navigation Timing L2][16], [High Resolution Time L2][17]).
The High Resolution Time specification went from an idea to fully implemented by
all major browser vendors and fully standardized in just 11 months. That must be
some sort of a record!

Looking back, the W3C was the perfect forum to bring together the top browser
vendors, web properties, and performance experts to discuss and try to solve
major performance issues. As web developers design more efficient web
applications and browser vendors design runtimes that can execute those web
applications more efficiently, we will all benefit from a faster and more
responsive web browsing experience.

Beyond the Web Performance Working Group, the W3C has [plans][18] to work with
the community to continue to enhance browsers, develop tools, improve education,
and promote performance in W3C specifications.

Let’s keep innovating. Follow the performance conversation in the Web
Performance Working Group!

[1]: http://channel9.msdn.com/Events/Build/2012/3-132
[2]: http://blogs.msdn.com/b/ie/archive/2010/08/18/microsoft-to-co-chair-new-w3c-web-performance-working-group.aspx
[3]: http://www.w3.org/TR/2012/REC-navigation-timing-20121217/
[4]: http://www.w3.org/TR/2012/CR-resource-timing-20120522/
[5]: http://www.w3.org/TR/2012/CR-user-timing-20120726/
[6]: http://www.w3.org/TR/2012/CR-performance-timeline-20120726/
[7]: http://www.w3.org/TR/hr-time/
[8]: http://www.w3.org/TR/animation-timing/
[9]: http://www.w3.org/TR/page-visibility/
[10]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/setImmediate/Overview.html
[11]: http://www.w3.org/2012/11/performance-workshop/
[12]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/ResourcePriorities/Overview.html
[13]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/Beacon/Overview.html
[14]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationErrorLogging/Overview.html
[15]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/ResourceErrorLogging/Overview.html
[16]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming2/Overview.html
[17]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/HighResolutionTime2/Overview.html
[18]: http://www.w3.org/2013/Talks/0610-performance/#/

[Bar chart showing browser subsystem load times in milliseconds for five sites]: img/MannFig2_lo.png