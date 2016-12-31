---
layout: page
title: About
---
## 競技プログラミング
* TopCoder: [jasy](https://www.topcoder.com/members/jasy)
* Codeforces: [jasy](http://www.codeforces.com/profile/jasy)
* AtCoder: [jasy](https://atcoder.jp/user/jasy)

## GitHub
{% for repo in site.github.public_repositories %}{% unless repo.fork %}
* [{{ repo.name }}]({{ repo.html_url }}): {{ repo.description }}{% endunless %}{% endfor %}
