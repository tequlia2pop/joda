# Joda-Time

http://www.joda.org/joda-time/

## 关于

Joda-Time 提供了 Java 日期和时间类的有效替换。

在 Java SE 8 之前，Joda-Time 是 Java 的事实上的标准日期和时间库。现在要求用户迁移到 `java.time`（JSR-310）。

Joda-Time 是根据 business-friendly 的 [Apache 2.0 许可证](http://www.joda.org/joda-time/license.html) 授权的。

## 功能

主要功能：

* `LocalDate` - 无时间的日期
* `LocalTime` - 无日期的时间
* `Instant` - 时间线上的某个精确的时刻
* `DateTime` - 完整的日期和时间，以及时区
* `DateTimeZone` - 一个更好的时区
* `Duration` 和 `Period` - 时间量
* `Interval` - 两个 instants 之间的时间
* 一个全面和灵活的格式化器-解析器（formatter-parser）

## 文档

提供了各种文档：

* [入门指南](http://www.joda.org/joda-time/quickstart.html)
* [用户指南](http://www.joda.org/joda-time/userguide.html)
* [关键概念](http://www.joda.org/joda-time/key.html) 和 [年表（chronology）指南](http://www.joda.org/joda-time/cal.html)
* [Javadoc](http://www.joda.org/joda-time/apidocs/index.html)
* [常见问题](http://www.joda.org/joda-time/faq.html)列表。
* 版本的[更改说明](http://www.joda.org/joda-time/installation.html)
* [GitHub](https://github.com/JodaOrg/joda-time) 源代码仓库

## 为什么选择 Joda Time？

Java SE 8 之前的标准日期和时间类较差。Joda-Time 成为 Java SE 8 之前 Java 的事实上的标准日期和时间库，从而解决了这个问题。**注意，从 Java SE 8 起，用户被要求迁移到 `java.time`（JSR-310） - 这是 JDK 的核心部分，它取代了这个项目。**

该设计允许多个日历系统，同时仍然提供一个简单的 API。 “默认”的日历是许多其他标准使用的 [ISO8601](http://www.joda.org/joda-time/cal_iso.html) 标准。还包括 Gregorian，Julian，Buddhist，Coptic，Ethiopic 和 Islamic 历法系统。支持类包括时区，持续时间，格式化和解析。

作为 Joda-Time 的风格，这里有一些示例代码：

````java
public boolean isAfterPayDay(DateTime datetime) {
  if (datetime.getMonthOfYear() == 2) {   // February is month 2!!
    return datetime.getDayOfMonth() > 26;
  }
  return datetime.getDayOfMonth() > 28;
}

public Days daysToNewYear(LocalDate fromDate) {
  LocalDate newYear = fromDate.plusYears(1).withDayOfYear(1);
  return Days.daysBetween(fromDate, newYear);
}

public boolean isRentalOverdue(DateTime datetimeRented) {
  Period rentalPeriod = new Period().withDays(2).withHours(12);
  return datetimeRented.plus(rentalPeriod).isBeforeNow();
}

public String getBirthMonthText(LocalDate dateOfBirth) {
  return dateOfBirth.monthOfYear().getAsText(Locale.ENGLISH);
}
````

## 理由

以下是我们开发和使用 Joda-Time 的一些原因：

* **使用方便。** Calendar 访问“正常”日期很困难，因为缺乏简单的方法。Joda-Time 有直接的 [字段访问器](http://www.joda.org/joda-time/field.html)，如 `getYear()` 或 `getDayOfWeek()`。
* **易于扩展。** JDK 通过 `Calendar` 的子类支持多个日历系统。这是笨重的，在实践中很难编写另一个日历系统。Joda-Time 通过基于 `Chronology` 类的插件系统支持多个日历系统。
* **综合功能集。**该库旨在提供日期时间计算所需的所有功能。它已经提供了开箱即用的功能，例如支持奇怪的日期格式，使用 JDK 很难实现。
* **最新的时区计算。**[时区的实现](http://www.joda.org/joda-time/timezones.html)基于公共 [tz 数据库](http://www.iana.org/time-zones)，它每年更新几次。新的 Joda-Time 版本包含对此数据库所做的所有更改。如果需要更早的更改，[手动更新区域数据](http://www.joda.org/joda-time/tz_update.html)很容易。
* **日历支持。**该库提供 [8 个日历系统](http://www.joda.org/joda-time/cal.html)。
* **轻松互操作。**该库内部使用了毫秒级的时刻（instant），其与 JDK 相同并且类似于其他公共时间表示。这使得互操作性变得容易，Joda-Time 具有开箱即用的 JDK 互操作性。
* **更好的性能特性。**日历具有奇怪的性能特征，因为它在意外的时刻重新计算字段。Joda-Time 只对被访问的字段进行最小计算。
* **良好的测试覆盖率。** Joda-Time 有一套全面的开发人员测试集，为库的质量提供了保证。
* **完整的文档。**有一份完整的[用户指南](http://www.joda.org/joda-time/userguide.html)，提供了概述，涵盖了常见的使用场景。[javadoc](http://www.joda.org/joda-time/apidocs/index.html) 非常详细，涵盖了 API 的其余部分。
* **发达。**该库自 2002 年以来一直在积极发展。它是一个成熟和可靠的代码库。现在有一些[相关项目](http://www.joda.org/joda-time/related.html)可用。
* **开源。** Joda-Time 由对商业友好的 [Apache License Version 2.0](http://www.joda.org/joda-time/license.html) 所许可。

## 发布

[版本 2.9.6](http://www.joda.org/joda-time/download.html) 是当前最新版本。这个版本被认为是稳定的，值得的 2.x 标签。有关详细信息，请参阅[升级说明](http://www.joda.org/joda-time/installation.html)。

Joda-Time 需要 Java SE 5 或更高版本，[没有依赖关系](http://www.joda.org/joda-time/dependencies.html)。对 Joda-Convert 有一个_编译时_依赖，但是这在运行时并不需要，因为注解的魔力。

在 [Maven Central](http://search.maven.org/#artifactdetails%7Cjoda-time%7Cjoda-time%7C2.9.6%7Cjar) 中可用。

````xml
<dependency>
  <groupId>joda-time</groupId>
  <artifactId>joda-time</artifactId>
  <version>2.9.6</version>
</dependency>
````

2.x 产品线将使用标准 Java 机制支持。主公共 API 将保持向后兼容 2.x 流中的源和二进制。版本号将更改为 3.0，以指示兼容性的重大更改。

Joda-Time v2.x是 1.x 代码库的演进，而不是主要的重写。它几乎完全源和二进制兼容 1.x 版本。主要更改包括使用Java SE 5 或更高版本，泛型和删除一些（但不是所有）已弃用的方法。有关从 1.x 升级的完整详细信息（包括不兼容的角落信息），请参阅[升级说明](http://www.joda.org/joda-time/upgradeto200.html)。老版本 [1.6.2](https://sourceforge.net/projects/joda-time/files/joda-time/1.6.2/) 是最后一个支持 Java SE 4 和最后一个 v1.x 版本的版本。