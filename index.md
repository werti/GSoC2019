## Project description

GStreamer is a framework for building multimedia applications. This framework allows you to create various applications. GStreamer has a plug-in architecture and has a very large set of plug-ins that can solve 99% of the needs of all multimedia developers. But until recently, GStreamer had only one metric for video quality --- DSSIM. The goal of my GSoC project was to create VMAF plugin for GStreamer.

VMAF is a new full-reference perceptual video quality metric developed by Netflix, which has a high correlation with subjective quality scores. It is open-source and ML-based metric, and it's base model is constantly updating. The developers add new features to each new version: such as 4K support, 95% confidence intervals, versions for measuring quality of displaying on phones and [other viewing options](https://github.com/Netflix/vmaf/releases/tag/v1.3.7).

## Short plugin description

The new iqa-vmaf plugin has been developed for GStreamer. It is based on GstVideoAggregator and supports all libvmaf options. It sends frame-by-frame results to pipeline via messages after EOS.

Additionally, in GStreamer, using the iqa-vmaf plugin, it is possible to calculate PSNR, SSIM, and MS-SSIM, since libvmaf can calculate them when calculating VMAF. Thus, the number of video quality metrics in GStreamer increased from one to five.

## Resources

### Repositories and description of writed code
* [gst-build-bad repository](https://gitlab.freedesktop.org/szve/gst-plugins-bad/):
  Old iqa plugin with DSSIM was renamed to iqa-dssim plugin and iqa-vmaf plugin was added. The iqa-vmaf plugin consists of this files:
  * [iqa-vmaf.h](https://gitlab.freedesktop.org/szve/gst-plugins-bad/blob/master/ext/iqa/iqa-vmaf.h)
  * [iqa-vmaf.c](https://gitlab.freedesktop.org/szve/gst-plugins-bad/blob/master/ext/iqa/iqa-vmaf.c)
  * [libvmaf_wrapper.h](https://gitlab.freedesktop.org/szve/gst-plugins-bad/blob/master/ext/iqa/libvmaf_wrapper.h)
  * [libvmaf_wrapper.cpp](https://gitlab.freedesktop.org/szve/gst-plugins-bad/blob/master/ext/iqa/libvmaf_wrapper.cpp)
  * [iqaplugin.c](https://gitlab.freedesktop.org/szve/gst-plugins-bad/blob/master/ext/iqa/iqaplugin.c)
* [gst-build repository](https://gitlab.freedesktop.org/szve/gst-build):
  The gst-build is auxiliary repository for GStreamer compilation. It use Meson build system and I created [wrapper](https://gitlab.freedesktop.org/szve/gst-build/blob/master/subprojects/vmaf.wrap) for VMAF submodule in it.
* [VMAF repository](https://github.com/werti/vmaf/tree/v1.3.14-gstreamer):
  To integrate VMAF into gst-build, I wrote a [meson configuration file](https://github.com/werti/vmaf/blob/v1.3.14-gstreamer/meson.build) for the VMAF project. I also made a [small patch](https://github.com/werti/vmaf/commit/b7ebb73cc6b432b0f44ef7d1381b082d4cbdf7e3#diff-fa18e21ed0ed7b3f769ceab3d86c7e3a) necessary for correct work with exceptions from libvmaf.

### Merge requests
 * Merge Request to [gst-plugins-bad](https://gitlab.freedesktop.org/gstreamer/gst-plugins-bad/merge_requests/520):
   Status (??-08-19) --
 * Merge Request to [gst-build](https://gitlab.freedesktop.org/gstreamer/gst-build/merge_requests/68):
   Status (??-08-19) --
 * Merge Request to [vmaf](https://github.com/Netflix/vmaf/pull/354):
   Status (??-08-19) --
