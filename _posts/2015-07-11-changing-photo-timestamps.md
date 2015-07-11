---
title: Changing Photo Timestamps
thumb: changing-photo-timestamps.png
author: Chris
---

Recently I came back from holiday and decided to import all my holiday snaps into the OSX photos application from my Nikon D3000 DSLR. Whilst I was away I had been taking some photos on my iPhone 6 which had already synced to my mac at home via iCloud. On completing the import I noticed that the DSLR photos were out of sync with my iPhone photos. At this point I realised I had forgotten to change the timezone!

Initially, I tried to resolve this by using the "Adjust Date and Time" feature of OSX Photos - however it turns out that this creates a new duplicate for each image, which will quickly fill up your hard drive.

#### Before:

![Timestamp Before](/images/timestamp-before.png)

To resolve this, I found a program called [exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/) which is a command line tool that allows for the manipulation of EXIF Data for images.

### Initial Attempts

{% highlight bash %}
$> exiftool "-AllDates+=1" DSC_0194.NEF
{% endhighlight %}

This command will create a new copy of the file (leaving the original safe for now), but increases the exif dates by 1 hour. 

Once happy with the changes, you can add `-overwrite_original_in_place` to save the changes permenantly over the original file.

#### Problem 1 - file dates are today

The downside to this is that the created/accessed/modified dates were all set to today

{% highlight bash %}
$> exiftool "-AllDates+=1" -p DSC_0194.NEF
{% endhighlight %}

The `-p` flag ensures that the original file dates were preserved.

#### Problem 2 - file modified/created/accessed dates are still in the wrong timezone

However this did not really solve the problem as OSX photos uses these still for ordering photos

{% highlight bash %}
$> exiftool "-AllDates+=1" -overwrite_original_in_place -DSC_0194.NEF
$> exiftool "-DateTimeOriginal>FileModifyDate" -overwrite_original_in_place DSC_0194.NEF
{% endhighlight %}

This time I increament the hour by 1, and then set the file modified date to be the same as the one in the EXIF data.

#### Problem 3 - file created date is not changing

This however left another problem, the created date would not change on OSX. To solve this I had to get a bit creative.

{% highlight bash %}
$> exiftool "-AllDates+=1" -overwrite_original_in_place -DSC_0194.NEF
$> exiftool "-DateTimeOriginal>FileModifyDate" -overwrite_original_in_place DSC_0194.NEF
$> SetFile -d "`GetFileInfo -m DSC_0194.NEF`" DSC_0194.NEF
{% endhighlight %}

This final command now gets the modified date for the file, and uses it to set the created date so they are all the same.

### The final solution

For the final solution, I wanted to be able to modify a whole folder of photos all at once, so I needed to do the following:

* Increment all the timestamps in the EXIF data by 1 Hour.
* Set the file modified date to be the same as the dates in the EXIF data.
* Set the created at date to be the same as the modified date.

{% highlight bash %}
$> exiftool "-AllDates+=1" -overwrite_original_in_place *.NEF
$> exiftool "-DateTimeOriginal>FileModifyDate" -overwrite_original_in_place *.NEF
$> for i in *.NEF; do SetFile -d "`GetFileInfo -m $i`" $i; done
{% endhighlight %}


#### The Result:

![Timestamp After](/images/timestamp-after.png)

