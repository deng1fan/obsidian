---
banner: "![[iShot_2023-04-06_10.07.12.png]]"
banner_y: 0.764
banner_x: 0.5
---

[Help Doc](https://obsidian-tasks-group.github.io/obsidian-tasks/queries/)

## 待办事项

```tasks
not done
NOT (path includes 个人/TODOs)
sort by due
```

## 正在进行中

```tasks
not done
status.name includes In Progress
sort by priority
```

## 今天已完成的事项

```tasks
done
done on today
```

---


## 今天即将截止事项:  

```ad-warning
title: Warning！
尽快完成下面的事项哦！

```

```tasks
((not done) AND (due on today))
is not recurring
sort by priority	
```

## 七天内即将截止的事项

```ad-example
title: 提醒
下面的事项马上就要截止了，合理规划时间哦！

```

```tasks
not done
(due before 7 days) AND NOT (due on today)
is not recurring
sort by priority	
```


## 超时事项

```ad-bug
title: 注意
下面事项可能需要进行必要的延时，否则应该马上放弃！

```

```tasks
not done
due before before today
is not recurring
```
