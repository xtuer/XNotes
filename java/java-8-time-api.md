java 8 提供的 时间api java.time 比原来的Calendar 方便很多，主要提供了:

* 日期类：LocalDate
* 时间类：LocateDateTime
* 时间戳操作类：Instant
* 时间持续时间计算：Duration
* 时区：ZoneId
* 日期间隔：Period

java 8 api 是整合了原第三方工具\(org.joda.time\)，使用将会更加方便。

```java
public static void main(String[] args) {
    Instant first = Instant.now();
    // Current Time
    LocalTime time = LocalTime.now();
    System.out.println("Current Time=" + time);
    // Creating LocalTime by providing input arguments
    LocalTime specificTime = LocalTime.of(12, 20, 25, 40);
    System.out.println("Specific Time of Day=" + specificTime);
    // Try creating time by providing invalid inputs
    // Current date in "Asia/Kolkata", you can get it from ZoneId javadoc
    LocalTime timeKolkata = LocalTime.now(ZoneId.of("Asia/Kolkata"));
    System.out.println("Current Time in IST=" + timeKolkata);

    // Getting date from the base date i.e 01/01/1970
    LocalTime specificSecondTime = LocalTime.ofSecondOfDay(10000);
    System.out.println("10000th second time= " + specificSecondTime);
    // 今日
    LocalDate localDate = LocalDate.now();
    System.out.println("今日日期:" + localDate);
    // Create
    LocalDate firstDay_2017 = LocalDate.of(2017, Month.JANUARY, 1);
    System.out.println("Specific Date=" + firstDay_2017);
    LocalDate hundredDay2017 = LocalDate.ofYearDay(2017, 200);
    System.out.println("200th day of 2017=" + hundredDay2017);
    // plus and minus operations
    System.out.println("昨天日期: " + localDate.minusDays(1));
    System.out.println("明天日期: " + localDate.plusDays(1));
    System.out.println("上月的今天：" + localDate.minusMonths(1));
    System.out.println("下个月的今天:" + localDate.plusMonths(1));
    // Temporal adjusters for adjusting the dates
    System.out.println("本月第1天的日期: " + localDate.with(TemporalAdjusters.firstDayOfMonth()));
    System.out.println("本月最后1天的日期: " + localDate.with(TemporalAdjusters.lastDayOfMonth()));
    System.out.println("本年最后1天的日期: " + localDate.with(TemporalAdjusters.lastDayOfYear()));
    // TemporalFieldfor adjusting the dates
    System.out.println("今天是：" + localDate.getYear() + "第" + localDate.get(ChronoField.ALIGNED_WEEK_OF_YEAR) + "周");
    System.out.println("今天是周: " + localDate.getDayOfWeek());
    System.out.println("今天是本周的第:" + localDate.getDayOfWeek().getValue() + "天");
    // before
    System.out.println("今天在20171001日之前：" + localDate.isBefore(LocalDate.of(2017, 10, 1)));
    // 格式化
    System.out.println("格式化：" + localDate.format(DateTimeFormatter.ofPattern("yyyy-MM-dd")));
    // Instant 时间戳转换
    System.out.println("当前时间:" + Instant.now().atZone(ZoneId.systemDefault()));
    System.out.println("当前的时间戳：" + Instant.now().toEpochMilli());
    System.out.println("时间戳转为时间字符串：" + Instant.ofEpochMilli(Instant.now().toEpochMilli()).atZone(ZoneId.systemDefault()));
    // Locale date time
    // Current Date
    LocalDateTime today = LocalDateTime.now();
    System.out.println("Current DateTime=" + today);

    // Current Date using LocalDate and LocalTime
    today = LocalDateTime.of(LocalDate.now(), LocalTime.now());
    System.out.println("Current DateTime=" + today);

    // Creating LocalDateTime by providing input arguments
    LocalDateTime specificDate = LocalDateTime.of(2014, Month.JANUARY, 1, 10, 10, 30);
    System.out.println("Specific Date=" + specificDate);

    // Current date in "Asia/Kolkata", you can get it from ZoneId javadoc
    LocalDateTime todayKolkata = LocalDateTime.now(ZoneId.of("Asia/Kolkata"));
    System.out.println("Current Date in IST=" + todayKolkata);

    // Getting date from the base date i.e 01/01/1970
    LocalDateTime dateFromBase = LocalDateTime.ofEpochSecond(10000, 0, ZoneOffset.UTC);
    System.out.println("10000th second time from 01/01/1970= " + dateFromBase);

    // Duration example
    Duration thirtyDay = Duration.ofDays(30);
    System.out.println("30天" + thirtyDay);

    // wait some time while something happens
    Instant second = Instant.now();
    // 计算两个时间，之间的长度 持续运行时间
    Duration duration = Duration.between(first, second);
    System.out.println("程序运行时间：" + duration);
    // 日期间隔计算
    Period period = localDate.until(localDate.with(TemporalAdjusters.lastDayOfYear()));
    System.out.println("Period Format= " + period);
    System.out.println("Months remaining in the year= " + period.getMonths());
}
```



