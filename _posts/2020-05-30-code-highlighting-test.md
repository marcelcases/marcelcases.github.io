---
layout: post
title: 'Code highlighting test'
author: marcel
category: projects
tags: code highlighting
published: false
date: 2020-05-30 12:25:00 +01:00
---

```python
class Byte:
    def __init__(self, tupla): # inicialitzador
        self.tupla = tupla

    def byte_to_int(self):
        self.tupla = self.tupla[::-1]
        acumulat = 0
        for i in range(7):
            acumulat += (self.tupla[i])*2**i
        return acumulat
```

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

~~~ ruby
def what?
  42
end
~~~

{% highlight ruby %}
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
{% endhighlight %}