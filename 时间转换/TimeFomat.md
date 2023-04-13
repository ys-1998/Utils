# 时间转换

## date =>string

```
 		Date createTime = video1.getCreateTime();//从数据库中获取到了Date类型的时间
        SimpleDateFormat simpleDateFormat=new SimpleDateFormat("yyyy:MM:dd HH:mm:ss");
        String format = simpleDateFormat.format(createTime);
```

## LocalDateTime =>String

```
	 LocalDateTime localDateTime=LocalDateTime.now();
        String format1 = localDateTime.format(DateTimeFormatter.ofPattern("yyyy:MM:dd HH:mm:ss"));
```



## String =>LocalDateTime(2048-12-12T12:12:12)

```
 		String time="2048-12-12 12-12-12";
        LocalDateTime parse = LocalDateTime.parse(time, DateTimeFormatter.ofPattern("yyyy-MM-dd HH-mm-ss"));
```



## String =>Date(Sat Dec 12 12:12:12 CST 2048)

```
Date date=null;
        try {
            String time2="2048-12-12 12-12-12";
            date= new SimpleDateFormat("yyyy-MM-dd HH-mm-ss").parse(time2);
        } catch (ParseException e) {
            e.printStackTrace();
        }
```

## 格式时间2022-12-01 00：00：00 转换时间戳格式

```
public class TimeUtil {

    public static long timeToStamp(String times){
        SimpleDateFormat simpleDateFormat=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String mytime=times;
        try {
            Date parse = simpleDateFormat.parse(mytime);
            long time = parse.getTime();
            return time;
        } catch (ParseException e) {
            e.printStackTrace();
        }

        return -1;
    }
}
```

##时间戳 格式时间 Date LocalDateTime

```
public class Demo {
    public static void main(String[] args) {
        //时间戳=》String 2013-03-12 00:00:00
        long l = System.currentTimeMillis();
        System.out.println(l);//1681357632892
        SimpleDateFormat formats=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String format = formats.format(l);
        System.out.println(format);//2023-04-13 11:47:12

        //String 2023-04-13 11:47:12 =>Date Thu Apr 13 11:47:12 CST 2023
        try {
            Date date = formats.parse(format);
            System.out.println(date);//Thu Apr 13 11:47:12 CST 2023
        } catch (ParseException e) {
            throw new RuntimeException(e);
        }

        LocalDateTime now = LocalDateTime.now();
        System.out.println(now);//2023-04-13T11:51:02.847
        String f1 = now.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"));
        System.out.println(f1);//2023-04-13 11:51:02
        
    }
}

```
