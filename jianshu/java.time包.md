# 概述

在JDK1.0中，Date类是唯一的一个代表时间的类，但是由于Date类不便于实现国际化，所以从JDK1.1版本开始，使用Calendar类进行时间和日期处理。
实际应用中，使用joda-time比较多（Java7以前），所以从Java8开始有了从joda改进的java.time包。
java.time 提供了用于日期、时间、实例和周期的主要API。
java.time包定义的类表示了日期-时间概念的规则，包括instants, durations, dates, times, time-zones and periods。这些都是基于ISO日历系统，它又是遵循 Gregorian规则的。
所有类都是不可变的、线程安全的。

# 常用类
Instant ：本质上是一个时间戳。
LocalDate ：存储了日期，如：2010-12-03。可以用来存储生日。
LocalTime ：存储了时间，如：11:30。
LocalDateTime ：存储了日期和时间，如：2010-12-03T11:30。
ZonedDateTime ：存储一个带时区的日期和时间。

方法概览：
该包的API提供了大量相关的方法，这些方法一般有一致的方法前缀：
of：静态工厂方法。
parse：静态工厂方法，关注于解析。
get：获取值。
is：用于比较。
with：不可变的setter等价物。
plus：加一些量到某个对象。
minus：从某个对象减去一些量。
to：转换到另一个类型。
at：把这个对象与另一个对象组合起来，例如：date.atTime(time)。

```java
        //获取当前日期时间
        LocalDateTime localDateTime = LocalDateTime.now();
        System.out.println("localDateTime :" + localDateTime);
        //格式化输出时间，线程安全的格式化类
        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy年MM月d日 hh:mm:ss");
        System.out.println("format :" + dateTimeFormatter.format(localDateTime));
        //  获取当前年份
        Year year = Year.of(2019);
        System.out.println("year :" + year);
        //   从Year获取LocalDate
        LocalDate localDate = year.atDay(41);
        System.out.println("localDate :" + localDate);
        //  把LocalTime关联到一个LocalDate得到一个LocalDateTime
        LocalTime localTime = LocalTime.of(12,0);
        LocalDateTime localDateTime1 = localTime.atDate(localDate);
        System.out.println("localDateTime1 :" + dateTimeFormatter.format(localDateTime1));
        //  判断是否是闰年
        System.out.println("isLeapYear :" + localDate.isLeapYear());
```
输出：
```
localDateTime :2019-02-10T22:30:05.581042500
format :2019年02月10日 10:30:05
year :2019
localDate :2019-02-10
localDateTime1 :2019年02月10日 12:00:00
isLeapYear :false
```

# 格式化与时间计算
DateTimeFormatter：在日期对象与字符串之间进行转换。
ChronoUnit：计算出两个时间点之间的时间距离，可按多种时间单位计算。
TemporalAdjuster：各种日期计算功能。

```java
DayOfWeek dayOfWeek = DayOfWeek.of(1);
        System.out.println("dayOfWeek :" + dayOfWeek);
        //计算两个日期之间时间，还可以按其他时间单位计算两个时间点之间的间隔。
        long between = ChronoUnit.HOURS.between(LocalDateTime.of(2019,2,10,22,0), LocalDateTime.of(2019,2,9,22,0));
        System.out.println("between :" + between);
        //  解析字符串形式的日期时间
        DateTimeFormatter dateTimeFormatter2 = DateTimeFormatter.ofPattern("yyyy MM d");
        TemporalAccessor temporalAccessor = dateTimeFormatter2.parse("2019 01 31");
        System.out.println("temporalAccessor :" + LocalDate.from(temporalAccessor));
        //计算某月的第一天的日期
        LocalDate with =  localDate.with(TemporalAdjusters.firstDayOfMonth());
        System.out.println("with :" + with);
        // 计算某月的第一个星期一的日期
        TemporalAdjuster temporalAdjuster = TemporalAdjusters.firstInMonth(DayOfWeek.MONDAY);
        LocalDate with1 = localDate.with(temporalAdjuster);
        System.out.println("with1 :" + with1);
        // 计算localDate的下一个星期一的日期
        LocalDate with2 = localDate.with(TemporalAdjusters.next(DayOfWeek.MONDAY));
        System.out.println("with2 :" + with2);
```
输出：

```
dayOfWeek :MONDAY
between :-24
temporalAccessor :2019-01-31
with :2019-02-01
with1 :2019-02-04
with2 :2019-02-11
```

# 新旧之间的转换
Date.toInstant()
Date.from(Instant)
Calendar.toInstant()

注意：输出instant时可能会出现与实际时间差8个小时的情况，这是因为Date和Calender输出时是按照中国所在的时区（UTC\GMT+8）输出的，而instant输出是按照相对于GMT的时间输出的，所以会相差8个小时。


