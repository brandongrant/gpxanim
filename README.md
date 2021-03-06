gpxanim
=======

`gpxanim` creates animated maps from GPX tracks.

It will plot the track as a line and rotate the map so that the
direction of travel is always "up".

The track is interpolated to achieve smooth animation.

Here is an example of its output: http://youtu.be/7-tOJGSVWkc


How it works
------------

1.  There are two components of `gpxanim`: a python script which
    controls the process, and a javascript module which updates the
    animation each frame.

2.  `gpxanim` uses the [OpenLayers][] javascript library to render the
    map tiles and GPX track.

3.  [WebKitGTK][] runs a small web page containing the map widget.

4.  Every frame, a screenshot is captured of the map and fed into a
    [GStreamer][] pipeline which creates an [Ogg Theora][] video file.

[OpenLayers]: http://www.openlayers.org/
[WebKitGTK]: http://webkitgtk.org/
[GStreamer]: http://gstreamer.freedesktop.org/
[Ogg Theora]: http://www.theora.org/

How to use
----------

First, get your track in GPX format. It would be better to have
correct speed and course values for the trackpoints. You can use
[GPSBabel][] to calculate the values:

    gpsbabel -i gpx -f bikehike.gpx \
        -x track,course -x track,speed \
        -o gpx -F synth.gpx

Then run

    python gpxanim.py synth.gpx

and it will start animating. It's not very fast unfortunately. At the
end you will have a video, called `synth.ogg` by default.

To see the full list of options, run

    python gpxanim.py --help

[GPSBabel]: http://www.gpsbabel.org/


Required packages (Debian/Ubuntu)
---------------------------------

    apt-get install python python-gtk2 python-webkit python-gst0.10 gstreamer0.10-ffmpeg gpsbabel gpsbabel-doc
