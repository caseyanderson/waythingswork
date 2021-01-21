---
layout: post
title:  "Kill Leftover screen Session (MacOS)"
date:   2020-09-02 06:00:00 -0630
week: ""
number: ""
categories: recipes
permalink: /:title.html
published: false
---

### MacOS

![]({{site.url}}/assets/failed_to_access_screen.png)

1. (in the Terminal) check to see if any there are any other active `screen sessions`: `screen -ls`

    ![]({{site.url}}/assets/imgs/screen_session_number.png)

2. write down the `session number` (13312 in the above image)
3. add the `session number` to the following command and hit ENTER to quit the leftover `screen` session: `screen -X -S 13312 quit`

