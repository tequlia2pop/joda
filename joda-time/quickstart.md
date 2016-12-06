# 入门

http://www.joda.org/joda-time/quickstart.html

本指南提供了 Joda-Time 的快速介绍。有关详细信息，请参阅完整的[用户指南](http://www.joda.org/joda-time/userguide.html)。

## 日期和时间

日期和时间是一个惊人的复杂领域。 Joda-Time 中的许多类被设计为允许完全表达域的细微差别。

最常使用的五个日期时间类是：

* [Instant](http://www.joda.org/joda-time/apidocs/org/joda/time/Instant.html) - 不可变类，表示时间线上的某个精确的时刻
* [DateTime](http://www.joda.org/joda-time/apidocs/org/joda/time/DateTime.html) - 不可变类，JDK `Calendar` 的替换
* [LocalDate](http://www.joda.org/joda-time/apidocs/org/joda/time/LocalDate.html) - 不可变类，表示不带时间的本地日期（无时区）
* [LocalTime](http://www.joda.org/joda-time/apidocs/org/joda/time/LocalTime.html) - 不可变类，表示没有日期的时间（无时区）
* [LocalDateTime](http://www.joda.org/joda-time/apidocs/org/joda/time/LocalDateTime.html) - 不可变类，表示本地日期和时间（无时区）

`Instant` 类可以很好地用于事件的时间戳，因为不必担心日历系统或时区。`LocalDate` 类可以很好地表示出生日期，因为没有必要参考一天的时间。`LocalTime` 可以很好地表示商店开门或关闭的时间。`DateTime` 类可以很好地类用作 JDK `Calendar` 类的通用替换，其中时区信息很重要。有关更多详细信息，请参阅关于 [instants](http://www.joda.org/joda-time/key_instant.html) 和 [partials](http://www.joda.org/joda-time/key_partial.html) 的文档。

## 使用日期和时间类

每个日期时间类都提供了各种构造函数。包括 `Object` 构造函数。这允许你从各种不同的对象构造一个实例：例如，`DateTime` 可以从以下对象构造：

* `Date` - a JDK instant
* `Calendar` - a JDK calendar
* `String` - ISO8601 格式
* `Long` - 毫秒
* 任何 Joda-Time 日期时间类

`Object` 构造函数的使用有一点不寻常，但它被使用是因为可以转换的类型的列表是可扩展的。主要的优点是从 JDK `Date` 或 `Calendar` 到 Joda-Time 类的转换很容易 - 只需将 JDK 类传递给构造函数即可。例如，此代码将`java.util.Date` 转换为 `DateTime`：

````java
java.util.Date juDate = new Date();
DateTime dt = new DateTime(juDate);
````

每个日期时间类提供了简单的方法来访问日期时间字段。例如，要访问月份和年份，你可以使用：

````java
DateTime dt = new DateTime();
int month = dt.getMonthOfYear();  // where January is 1 and December is 12
int year = dt.getYear();
````

所有主日期时间类都是不可变的，就像 `String`，并且在创建后不能更改。然而，已经提供了简单的方法来改变新创建的对象中的字段值。例如，要设置年份，或添加2小时，你可以使用：

````java
DateTime dt = new DateTime();
DateTime year2000 = dt.withYear(2000);
DateTime twoHoursLater = dt.plusHours(2);
````

除了基本的 get 方法之外，每个日期时间类都为每个字段提供了属性方法 这些提供了丰富的 Joda-Time 功能。例如，要访问有关一个月或一年的详细信息：

````java
DateTime dt = new DateTime();
String monthName = dt.monthOfYear().getAsText();
String frenchShortName = dt.monthOfYear().getAsShortText(Locale.FRENCH);
boolean isLeapYear = dt.year().isLeap();
DateTime rounded = dt.dayOfMonth().roundFloorCopy();
````

## 日历系统和时区

Joda-Time 支持多个[日历系统](http://www.joda.org/joda-time/key_chronology.html)和全范围的时区。[Chronology](http://www.joda.org/joda-time/apidocs/org/joda/time/Chronology.html) 和 [DateTimeZone](http://www.joda.org/joda-time/apidocs/org/joda/time/DateTimeZone.html) 类提供了此支持。

Joda-Time 默认使用 ISO 日历系统，这是世界使用的事实上的民用日历。默认时区与 JDK 的默认时区相同。这些默认值可以在必要时被覆盖。请注意，ISO 日历系统在 1583 年之前的历史上并不准确。

Joda-Time 使用日历的可插拔机制。相比之下，JDK 使用子类，如 `GregorianCalendar`。此代码通过调用`Chronology` 实现上的一个工厂方法来获得 Joda-Time 年表：

````java
Chronology coptic = CopticChronology.getInstance();
````

时区作为年表的一部分实现。获得 Tokyo 时区的 Joda-Time 年表的代码：

````java
DateTimeZone zone = DateTimeZone.forID("Asia/Tokyo");
Chronology gregorianJuian = GJChronology.getInstance(zone);
````

## 间隔和时间段

Joda-Time 支持间隔和时间段。

[间隔（interval）](http://www.joda.org/joda-time/key_interval.html)由 [`Interval`](http://www.joda.org/joda-time/apidocs/org/joda/time/Interval.html) 类表示。它保存开始和结束日期时间，并允许基于该时间范围的操作。

[时间段(time period)](http://www.joda.org/joda-time/key_period.html) 由 [`Period`](http://www.joda.org/joda-time/apidocs/org/joda/time/Period.html) 类表示。可以持有诸如6个月，3天和7小时的 period。你可以直接创建 `Period`，或从 interval 中派生。

[持续时间(time duration)](http://www.joda.org/joda-time/key_duration.html)由 [Duration](http://www.joda.org/joda-time/apidocs/org/joda/time/Duration.html) 类表示。它保存精确的 duration（以毫秒为单位）。你可以直接创建 Duration，或从 interval 中派生。

虽然 period 和 duration 看起来相似，但它们的工作方式不同。例如，考虑在夏令时切换时向 DateTime 添加一天：

````java
DateTime dt = new DateTime(2005, 3, 26, 12, 0, 0, 0);
DateTime plusPeriod = dt.plus(Period.days(1));
DateTime plusDuration = dt.plus(new Duration(24L*60L*60L*1000L));
````

在这种情况下添加 period 将增加 23 小时，而不是 24 因为夏令时更改，因此结果的时间仍将是中午。添加 duration 将增加 24 小时，无论什么，因此结果的时间将更改为 13:00。

## 更多信息

有关详细信息，请参阅以下内容：

* [完整的用户指南](http://www.joda.org/joda-time/userguide.html)
* [关键概念](http://www.joda.org/joda-time/key.html)
* 可用的[日历系统](http://www.joda.org/joda-time/cal.html)
* [常见问题](http://www.joda.org/joda-time/faq.html)
* [Javadoc](http://www.joda.org/joda-time/apidocs/index.html)