# Date

https://mp.weixin.qq.com/s/v-Va_GuSUGr9HVAW84kloQ

+ Date
  + 很多方法现在都已经弃用
  + 可变类
  + SimpleDateFormat 线程不安全
+ LocalDateTime
  + 不可变、线程安全
  + DateTimeFormatter 线程安全

https://stackoverflow.com/questions/58456737/creating-date-objects-in-kotlin-for-api-level-less-than-or-equal-to-16

Never use Date, Calendar, or SimpleDateFormat