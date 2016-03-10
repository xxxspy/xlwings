---
layout: landingpage
title: xlwings

box_title: Why xlwings is awesome
box: |
    * **Easy deployment**: The receiver of an xlwings-powered spreadsheets only needs [Python][] with minimal
      [dependencies][] &mdash; or nothing at all when shipped with the Python runtime.
    * **Cross-Platform**: xlwings works with Microsoft Excel on Windows and Mac.
    * **Plug-and-Play**: No cumbersome installation of Excel add-ins or license keys.
    * **Flexible**: Works with pretty much every combination of Excel and Python.
    * **Two way communication**: Call Python from Excel or interact with Excel from Python.
    * **User Defined Functions (UDFs)**: Supported on Windows.
    * **Free and open-source**: xlwings is released under a permissive [BSD-License][].

    [Python]: http://www.python.org
    [BSD-License]: http://opensource.org/licenses/BSD-3-Clause
    [dependencies]: http://docs.xlwings.org/installation.html#dependencies
---

# Make Excel fly with Python!

## Replace your VBA code with Python, a powerful yet easy-to-use programming language that is highly suited for numerical analysis. Supports Windows & Mac!

#### Latest Release v0.7.0 (March 4, 2016): New converters: e.g. use DataFrames from UDFs and Range objects! see [release notes][] for details.

#### Watch <a href="https://zoomeranalytics.wistia.com/medias/ovf3k3u4w9" target="_blank">this 2-min video</a> to see UDFs with DataFrames in action!

#### Shape the future of xlwings: <a href="https://zoomeranalytics.uservoice.com/forums/269851-xlwings" target="_blank">xlwings feature requests</a>.

[release notes]: http://docs.xlwings.org/en/stable/whatsnew.html
[watch!]: https://twitter.com/ZoomerAnalytics/status/664159348822835200

<div class="row">
  <div class="col-lg-3">
  </div>
    <div class="col-lg-6">
      <div class="video-container">
<iframe src="//fast.wistia.net/embed/iframe/fb3pft6wdu?videoFoam=true" allowtransparency="true" frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" allowfullscreen mozallowfullscreen webkitallowfullscreen oallowfullscreen msallowfullscreen width="640" height="400"></iframe><script src="//fast.wistia.net/assets/external/iframe-api-v1.js"></script>
      </div>
    </div>
</div>

**Note**: The video has been made for v0.1.0 and is now outdated in various places, amongst them are:

* The line `In [24]` should now read: `Range('A2', wkb=wb).options(np.array, expand='table').value`
* At minute 4.47: Line 4 should be replaced with `wb = Workbook.caller()` and moved within the function definition.