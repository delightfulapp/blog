title: Multiple photos selection for Delightful Upload feature
date: 2014-11-30 10:07:54
tags:
- ios
- development

---

For Deligthful upload feature, there are some features I want to have when selecting photos:

1. Drag to select multiple photos quickly.
2. Being able to preview a photo. Either by tap and hold the photo or pinch out the photo.

<!--more-->

I chose to use the new Photos framework instead of Assets Library since Delightful only supports iOS 8 or later. Another thing is I chose to use the new UISplitViewController since it now is available on the iPhone. And using UISplitViewController, albums and photos apear side by side in landscape mode. The result is [DLFPhotosPicker](https://github.com/nicnocquee/DLFPhotosPicker).

![](https://raw.githubusercontent.com/nicnocquee/DLFPhotosPicker/master/screenshots/iOS%20Simulator%20Screen%20Shot%20Nov%2030,%202014,%2009.38.34.png)

I'd like include DLFPhotosPicker in cocoapods but I still haven't figured out how to include PhotosPicker.storyboard in the pod. Any advice is greatly appreciated.

{% rawblock %}
<p align="center">
<video width="320" controls>
  <source src="http://f.cl.ly/items/2K1m2f2W1L1v0a090o0q/demo-11.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>
</p>
{% endrawblock /%}