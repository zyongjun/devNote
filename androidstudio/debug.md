#### TimingLogger
private TimingLogger loger = new TimingLogger("debug","initProject");

loger.addSplit("start");
loger.addSplit("-----init managerImageobj");
loger.addSplit("start load drawobj");

E:\androidcode\coderead\Tuto>adb shell setprop log.tag.debug VERBOSE


09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject: begin
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject:      16 ms, start
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject:      32 ms, -----init managerImageobj
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject:      15 ms, start copy 1
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject:      105 ms, start copy 2
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject:      2452 ms, start copy 3
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject:      0 ms, end copy
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject:      1 ms, start load drawobj
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject:      203 ms, end load draw obj
09-16 16:56:33.994 3460-3460/com.windhike.tuto D/debug: initProject: end, 2824 ms