
# What is this?

This repo attempts to reproduce a possible issue with Shaka 3.2.0.
# Quickstart
Requires Node v10+
```
npm install
npm run start
```
This serves the static directory with a delay of 300ms for all files. Then, open http://localhost:8000, and view the network tab, and you should see something like this:

![chrome screenshot](./chrome_screenshot.png.png)


(This is on Chrome This is on Chrome 95.0.4638.54)
# The Issue
When initially loading a manifest, we pass in a time via the documented api for `player.load()` (the second argument). If we then use the video element API to request a seek without waiting for the segment to finish loading, we see a large number of cancelled and restarted requests (usually, exactly 11 requests) for the same segment within a short timeframe-- even if we only request a seek once, and even if the requested seek lies within the same segment which is ar


First, some context. We are building a browser-based video editor, and we are using a proprietary technique to generate DASH segments just-in-time on a backend so that when users upload files to our systems, they can be played back and scrubbed without having to wait for a blocking DASH transmux.
