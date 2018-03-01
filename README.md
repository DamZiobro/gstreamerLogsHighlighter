GStreamer Logs Vim Highlighter
========

Vim syntax file which allows to add color highlighting when you watch GStreamer
logs in vim (see picture below)

Installation
========
   1. Place gstreamer_highlight_syntax.vim file to your $HOME/.vim/syntax directory
   2. Put following line somewhere into your $HOME/.vimrc file: 
      au BufNewfile,BufRead syslog*.log set filetype=gstreamer_highlight_syntax

Usage
========
1. Run you gstreamer application and redirect logs into syslog:
```
GST_DEBUG=*:2,filesink:5,ringbuffer:2,videotestsrc:5,videoconvert:5,queue:5,theoraenc:5,oggmux:5 timeout 10s gst-launch-1.0 videotestsrc ! queue ! videoconvert ! theoraenc ! queue ! oggmux name=mux autoaudiosrc ! queue ! audioconvert ! vorbisenc ! queue ! mux. mux. !  queue ! filesink location=test.ogg 2> >(logger -t gst-launch)

```
2. Filter syslog logs from your application (in our case gst-launch) and save
   into separate file which name starts with 'syslog' (notice 'syslog'-based pattern Installation section):
```
grep gst-launch /var/log/syslog > /tmp/syslog
```
3. Open created file in vim - you should see colorful GStreamer logs if your
   file name starts with 'syslog'

Example logs highlighting
=========
![highlighter(https://raw.githubusercontent.com/xmementoit/gstreamerLogsHighlighter/master/gstreamerVimHighlight.png
