joda-time-2.2.jar
=================

Joda-Time提供了一组Java类包用于处理包括ISO8601标准在内的date和time。可以利用它把JDK Date和Calendar类完全替换掉，而且仍然能够提供很好的集成。

http://joda-time.sourceforge.net/ 

版本：joda-time.jar 

1、时间类得作成 



Java代码  
1.//方法一：取系统点间  
2.DateTime dt1 = new DateTime();  
3.  
4.//方法二：通过java.util.Date对象生成  
5.DateTime dt2 = new DateTime(new Date());  
6.  
7.//方法三：指定年月日点分秒生成(参数依次是：年,月,日,时,分,秒,毫秒)  
8.DateTime dt3 = new DateTime(2012, 5, 20, 13, 14, 0, 0);  
9.  
10.//方法四：ISO8601形式生成  
11.DateTime dt4 = new DateTime("2012-05-20");  
12.DateTime dt5 = new DateTime("2012-05-20T13:14:00");  
13.  
14.//只需要年月日的时候  
15.LocalDate localDate = new LocalDate(2009, 9, 6);// September 6, 2009  
16.  
17.//只需要时分秒毫秒的时候  
18.LocalTime localTime = new LocalTime(13, 30, 26, 0);// 1:30:26PM  
 

2、获取年月日点分秒 



Java代码  
1.DateTime dt = new DateTime();  
2.//年  
3.int year = dt.getYear();  
4.//月  
5.int month = dt.getMonthOfYear();  
6.//日  
7.int day = dt.getDayOfMonth();  
8.//星期  
9.int week = dt.getDayOfWeek();  
10.//点  
11.int hour = dt.getHourOfDay();  
12.//分  
13.int min = dt.getMinuteOfHour();  
14.//秒  
15.int sec = dt.getSecondOfMinute();  
16.//毫秒  
17.int msec = dt.getMillisOfSecond();  
 

3、星期的特殊处理 



Java代码  
1.DateTime dt = new DateTime();  
2.  
3.//星期  
4.switch(dt.getDayOfWeek()) {  
5.case DateTimeConstants.SUNDAY:  
6.    System.out.println("星期日");  
7.    break;  
8.case DateTimeConstants.MONDAY:  
9.    System.out.println("星期一");  
10.    break;  
11.case DateTimeConstants.TUESDAY:  
12.    System.out.println("星期二");  
13.    break;  
14.case DateTimeConstants.WEDNESDAY:  
15.    System.out.println("星期三");  
16.    break;  
17.case DateTimeConstants.THURSDAY:  
18.    System.out.println("星期四");  
19.    break;  
20.case DateTimeConstants.FRIDAY:  
21.    System.out.println("星期五");  
22.    break;  
23.case DateTimeConstants.SATURDAY:  
24.    System.out.println("星期六");  
25.    break;  
26.}  
 

4、与JDK日期对象的转换 



Java代码  
1.DateTime dt = new DateTime();  
2.  
3.//转换成java.util.Date对象  
4.Date d1 = new Date(dt.getMillis());  
5.Date d2 = dt.toDate();  
6.  
7.//转换成java.util.Calendar对象  
8.Calendar c1 = Calendar.getInstance();  
9.c1.setTimeInMillis(dt.getMillis());  
10.Calendar c2 = dt.toCalendar(Locale.getDefault());  
 

5、日期前后推算 



Java代码  
1.DateTime dt = new DateTime();  
2.  
3.//昨天  
4.DateTime yesterday = dt.minusDays(1);         
5.//明天  
6.DateTime tomorrow = dt.plusDays(1);       
7.//1个月前  
8.DateTime before1month = dt.minusMonths(1);        
9.//3个月后  
10.DateTime after3month = dt.plusMonths(3);          
11.//2年前  
12.DateTime before2year = dt.minusYears(2);          
13.//5年后  
14.DateTime after5year = dt.plusYears(5);  
 

6、取特殊日期 



Java代码  
1.DateTime dt = new DateTime();     
2.  
3.//月末日期    
4.DateTime lastday = dt.dayOfMonth().withMaximumValue();  
5.  
6.//90天后那周的周一  
7.DateTime firstday = dt.plusDays(90).dayOfWeek().withMinimumValue();  
 

7、时区 



Java代码  
1.//默认设置为日本时间  
2.DateTimeZone.setDefault(DateTimeZone.forID("Asia/Tokyo"));  
3.DateTime dt1 = new DateTime();  
4.  
5.//伦敦时间  
6.DateTime dt2 = new DateTime(DateTimeZone.forID("Europe/London"));  
 

8、计算区间 



Java代码  
1.DateTime begin = new DateTime("2012-02-01");  
2.DateTime end = new DateTime("2012-05-01");  
3.  
4.//计算区间毫秒数  
5.Duration d = new Duration(begin, end);  
6.long time = d.getMillis();  
7.  
8.//计算区间天数  
9.Period p = new Period(begin, end, PeriodType.days());  
10.int days = p.getDays();  
11.  
12.//计算特定日期是否在该区间内  
13.Interval i = new Interval(begin, end);  
14.boolean contained = i.contains(new DateTime("2012-03-01"));  
 

9、日期比较 



Java代码  
1.DateTime d1 = new DateTime("2012-02-01");  
2.DateTime d2 = new DateTime("2012-05-01");  
3.  
4.//和系统时间比  
5.boolean b1 = d1.isAfterNow();  
6.boolean b2 = d1.isBeforeNow();  
7.boolean b3 = d1.isEqualNow();  
8.  
9.//和其他日期比  
10.boolean f1 = d1.isAfter(d2);  
11.boolean f2 = d1.isBefore(d2);  
12.boolean f3 = d1.isEqual(d2);  
 

10、格式化输出 



Java代码  
1.DateTime dateTime = new DateTime();  
2.  
3.String s1 = dateTime.toString("yyyy/MM/dd hh:mm:ss.SSSa");  
4.String s2 = dateTime.toString("yyyy-MM-dd HH:mm:ss");  
5.String s3 = dateTime.toString("EEEE dd MMMM, yyyy HH:mm:ssa");  
6.String s4 = dateTime.toString("yyyy/MM/dd HH:mm ZZZZ");  
7.String s5 = dateTime.toString("yyyy/MM/dd HH:mm Z");  
