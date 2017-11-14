# NewPage & Tags

## 1 new page

```markdown
hexo new newpage
``` 
> * in `/hexo-dir/source/_posts` dicrectory create `newpage.md`

## 2 new Tag

* 1 create new page

```
hexo new page tags
``` 

* 2 mark tags

```
---
title: tag test
date: 2017-11-14 21:44:33
type: "tags"
---
```

* 3 edit theme config

```
menu:
  home: /
  archives: /archives
  tags: /tags
```

* 4 delete tags 

```
hexo clean
hexo s --debug
```
